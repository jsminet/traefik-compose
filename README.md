
## <p align="center">Traefik base configuration on Swarm</p>
    
## 🧐 Features    
- Using docker compose version 2
- Traefik as an tcp/http edge proxy
- Docker secret (that's why swarm is **mandatory**)
        
## 🛠️ Tech Stack
- [Traefik](https://doc.traefik.io/traefik/)


## ⚡ File generation

### Compose file for swarm

The first step is to generate a compose file compliant with Docker Swarm.

**Warning:** Due to json incompatibility between docker compose and docker swarm specifications, you must convert some tags, here is an example using linux sed command

```Bash
docker compose config | sed '/published:/s/\"//g' | sed '/^name:/d' | sed -E 's/(cpus*[^:]+:)\s*([^"#\n]+)$/\1 "\2"/' > traefik-stack.yml
```
The **stack.yml** generated file is ready to deploy on a Swarm cluster (see Usage below)

### Docker secret

- Windows gitbash

```bash
openssl rand -base64 20 | docker secret create traefik_basicauth -
```
- Linux shell
```bash
echo $(htpasswd -nb username password) | sed -e s/\\$/\\$\\$/g
```

## 🧑🏻‍💻 Usage

### Managing the stack

```Bash
# Swarm initialization
$ docker swarm init
```
```Bash
# Starting the stack
$ docker stack deploy -c traefik-stack.yml traefik
```
```Bash
# Stopping the stack
$ docker stack rm traefik
```
```Bash
# Cleaning all volumes
$ docker compose down -v
```
       
## 🙇 Author
#### JS
- Github: [@jsminet](https://github.com/jsminet)
        
## ➤ License
Distributed under the MIT License. See [LICENSE](LICENSE) for more information.
        
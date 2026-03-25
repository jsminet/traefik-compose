Create a file you must name *usersfile* for traefik dashboard access with basicauth

Create hash password
- Windows gitbash
```bash
openssl rand -base64 20 | docker secret create traefik_basicauth -
```

- Linux shell
```bash
echo $(htpasswd -nb username password) | sed -e s/\\$/\\$\\$/g
```
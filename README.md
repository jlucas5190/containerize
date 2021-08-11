# Containerize

## Containerize a Python application


### Part One

Complete the provided `nginx/nginx.conf` by writing a `server` directive(s) that proxies to the upstream application.

Requirements:

- Nginx should accept requests on ports 80 and 443
- All HTTP requests should permanently redirect to their HTTPS equivalent
- Use the provided SSL keypair found in `nginx/files/localhost.crt` and `nginx/files/localhost.key` for your SSL configuration
- Ensure the SSL keypair is available to nginx, but is not baked in to the container image
- The SSL configuration should use modern and secure protocols and ciphers
- Nginx should proxy requests to the application using an `upstream` directive
- Pass headers `X-Forwarded-For`, `X-Real-IP`, and `X-Forwarded-Proto` to the upstream application with appropriate values

### Part Two

Complete `app/Dockerfile`, `nginx/Dockerfile` and `docker-compose.yml` to produce a production ready image that can be also be used for development with Compose.

Requirements:

- The app found in `./app/src` is securely built, installed, and configured into a container.
- When run by itself, the app container should start the app, serving traffic with a production quality server, on port `8000` without any extra configuration.
- Running `docker-compose up` should:
  - Start the app container in development mode listening on port `8000`
  - Allow local edits of the app source to be reflected in the running app container without restart (eg: hot code reload)
  - Start an nginx container configured with the files from Part One
  - The `app` service should not reachable directly from the host and can only be accessed through the `nginx` service.

## Tying it all together

After running `docker-compose up` a command such as `curl -k https://localhost/` should return output similar to:

```Text
It's easier to ask forgiveness than it is to get permission.
X-Forwarded-For: 172.20.0.1
X-Real-IP: 172.20.0.1
X-Forwarded-Proto: https
```

You may also run the included validation tool to further test your work. This script will stop and remove running and built containers, so _please be careful._ You can run the tool like so:

```shell
# Stop, remove, rebuild containers, and run tests (see -h for help)
./validate.sh
```


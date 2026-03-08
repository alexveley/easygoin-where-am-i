# Where Am I?

A minimal web app: one button to get your GPS coordinates, then copy them with one click.

- **Get my location** — requests browser GPS permission and shows latitude, longitude.
- **Copy** — copies the coordinates to the clipboard.

Works in modern browsers over HTTPS (or localhost). Safe to host on any static site (GitHub Pages, Netlify, etc.).

## Run locally

Open `index.html` in a browser, or serve the folder:

```bash
# Python
python -m http.server 8000

# Node (npx)
npx serve .
```

Then visit `http://localhost:8000` (use HTTPS or localhost so geolocation is allowed).

## Docker / Portainer

Build and run with Docker Compose:

```bash
docker compose up -d --build
```

App listens on port 80 inside the container. No host port is published—attach a reverse proxy (e.g. Traefik, Caddy, Nginx Proxy Manager) to the stack’s network and route to the `web` service.

### Deploy as a stack in Portainer

1. In Portainer: **Stacks** → **Add stack**.
2. Name the stack (e.g. `easygoin-where-am-i`).
3. Under **Build method**, choose **Repository**.
4. Set **Repository URL** to your repo:  
   `https://github.com/alexveley/easygoin-where-am-i`
5. Set **Compose path** to `docker-compose.yml` (or leave default if it picks it up).
6. Click **Deploy the stack**.

Put the stack on the same Docker network as your reverse proxy and route your chosen host/subdomain to the `web` service (port 80). Use HTTPS so geolocation works in the browser.

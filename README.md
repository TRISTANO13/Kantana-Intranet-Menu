# Kantana Intranet Menu

This repository provides a **simple, single‑page intranet launcher** to centralize access to internal tools and services. It is intentionally lightweight – just one `index.html` file served with Nginx – but it includes useful features like search, tag filtering, favorites (saved in the browser), and service status checks.

---

## ✨ Features

* **Service cards** with name, URL, icon, tags, and category.
* **Search bar**: filter services by name, tags, or URL.
* **Tag filtering**: click tags to narrow down the view.
* **Favorites**: mark frequently used services (saved in `localStorage`).
* **Status check**: basic health check of services via `fetch()`.
* **Responsive design**: grid layout adapts to screen size.

---

## 🚀 Quick Start

### Local (no Docker)

1. Clone this repository:

   ```bash
   git clone https://github.com/TRISTANO13/Kantana-Intranet-Menu.git
   cd Kantana-Intranet-Menu
   ```
2. Open `index.html` directly in your browser **or** serve it with a local HTTP server:

   ```bash
   npx http-server -p 8080
   ```
3. Visit [http://localhost:8080](http://localhost:8080).

### With Docker Compose

A `docker-compose.yaml` is included:

```yaml
services:
  intranet:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./:/usr/share/nginx/html:ro
    restart: unless-stopped
    container_name: intranet-menu
```

Run with:

```bash
docker compose up -d
```

Then open [http://localhost](http://localhost).

---

## ⚙️ Configuration

All services are defined inside `index.html` in the `SERVICE_LIST` constant:

```js
const SERVICE_LIST = [
  { name:"Wiki (Wiki.js)", url:"http://tools.cg.kantana.co.th:8001", icon:"📄", tags:["Docs","Information"], category:"Documentation"},
  { name:"Ayon", url:"http://tools.cg.kantana.co.th:8002", icon:"🎞️", tags:["VFX","Pipeline"], category:"Tools"},
  { name:"Asset Library", url:"http://tools.cg.kantana.co.th:8003", icon:"📚", tags:["Resources","3D"], category:"Tools"},
  { name:"Excalidraw (Under development)", url:"http://tools.cg.kantana.co.th:8004", icon:"✏️", tags:["Whiteboard","Collaborative"], category:"Tools"}
];
```

* **name** → display name.
* **url** → target service URL.
* **icon** → emoji or text shown in the card.
* **tags** → used for filtering.
* **category** → groups services (optional, defaults to *Misc*).
* **health** → optional path (e.g. `/health`) for more accurate status check.

---

## 🖌️ Customization

* **Colors & theme**: controlled via CSS variables in the `<style>` section.
* **Layout**: grid size and card design defined in CSS.
* **Language**: all interface text is in English.

---

## 📡 Status Checks

* Uses `fetch()` from the browser.
* By default, `mode: no-cors` is used (many responses show as *opaque* but still prove reachability).
* For accurate status (HTTP codes), enable CORS on your services’ `/health` endpoints.

---

## 🛠️ Troubleshooting

* **Status always “Unknown”** → services block CORS; add a `/health` endpoint or run launcher under the same domain.
* **Favorites not saving** → check that your browser allows `localStorage`.
* **No services showing** → ensure `SERVICE_LIST` is filled correctly.

---

## 🤝 Contributing

1. Fork the repo.
2. Create a feature branch.
3. Commit changes with clear messages.
4. Open a pull request.

---

## 📜 License

This project is provided as‑is. If you need a formal license, add a `LICENSE` file (MIT recommended).

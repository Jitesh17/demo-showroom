![Astro](https://img.shields.io/badge/Astro-Static%20Site-ff5d01?logo=astro)
![Cloudflare Pages](https://img.shields.io/badge/Cloudflare-Pages-f38020?logo=cloudflare)
![Deployment](https://img.shields.io/badge/Deploy-Automatic-success)
[![Live](https://img.shields.io/badge/Live-demos.jiteshgosar.com-blue)](https://demos.jiteshgosar.com)

# Demo Showroom

A lightweight **demo showroom** built with **Astro** and deployed on **Cloudflare Pages**.  
It serves as a clean, fast front door to showcase **live, runnable demos** hosted on a laptop or server and securely exposed using **Cloudflare Tunnel**.

The goal is simple:
- One public place to see all demos
- Each demo has context, visuals, and a clear entry point
- Demos can be started and stopped on demand

---

## 🌍 Live URLs

| Item | URL |
|---|---|
| Showroom UI | https://demos.jiteshgosar.com |
| Jellyfin Demo | https://media.jiteshgosar.com |

---

## 🧠 What This Project Is (and Is Not)

**This project is:**
- A static UI layer
- A catalogue of demos
- A control surface to access running services

**This project is NOT:**
- A backend service
- A container orchestration system
- A place to store secrets or credentials

All demo services run separately and are exposed via Cloudflare.

---

## 🧭 High-Level Architecture

The system is intentionally simple and reliable.

```
Browser
  → Cloudflare Pages (Static UI)
     → Cloudflare Tunnel
        → Local service (systemd / container / script)
```

### Responsibility split

| Layer | Responsibility |
|---|---|
| Astro UI | Presentation, navigation, documentation |
| Cloudflare Pages | Hosting, TLS, global CDN |
| Cloudflare Tunnel | Secure inbound access |
| Local machine | Running demo services |

---

## 📁 Repository Structure

| Path | Purpose |
|---|---|
| public/images | Demo thumbnails and assets |
| src/pages/index.astro | Showroom landing page |
| src/pages/demos/[slug].astro | Individual demo pages |
| src/components | UI components |
| docs | Operational documentation |

---

## 🚀 Local Development

Install dependencies:
```bash
npm install
```

Run local dev server:
```bash
npm run dev
```

Local URL:
```
http://localhost:4321
```

---

## 🏗️ Build

```bash
npm run build
```

Output:
```
dist/
```

This project is fully static.

---

## ☁️ Deployment (Cloudflare Pages)

Deployment is automatic.

| Setting | Value |
|---|---|
| Platform | Cloudflare Pages |
| Git branch | main |
| Build command | npm run build |
| Output directory | dist |
| Trigger | Push to main |

No deploy scripts are stored in this repo.

---

## 🌐 DNS & Subdomains

DNS and TLS are handled entirely by Cloudflare.

| Subdomain | Target | Purpose |
|---|---|---|
| demos.jiteshgosar.com | Cloudflare Pages | Showroom UI |
| media.jiteshgosar.com | Cloudflare Tunnel | Jellyfin demo |

Each demo can use its own subdomain.

---

## 🎬 Demo Example: Jellyfin

**What it is:**  
Self-hosted media server demo.

**How it runs:**  
- Managed by systemd
- Exposed via Cloudflare Tunnel
- Accessed through the showroom

### Service control

| Action | Command |
|---|---|
| Start | sudo systemctl start jellyfin |
| Stop | sudo systemctl stop jellyfin |
| Restart | sudo systemctl restart jellyfin |
| Restart tunnel | sudo systemctl restart cloudflared |

---

## ➕ Adding a New Demo

The process is repeatable and intentionally manual.

### 1. Create a demo page
```
src/pages/demos/<demo-name>.astro
```

Include:
- Description
- Screenshot or video
- Live URL
- Notes or limitations

### 2. Run the service
- systemd service
- container
- or standalone process

### 3. Expose it
- Create Cloudflare Tunnel
- Assign subdomain

### 4. Register it
- Add demo card to the landing page
- Commit and push

---

## 🔐 Access Model

| Aspect | Current | Future |
|---|---|---|
| Public access | Yes | Yes |
| Authentication | App-level | Time-limited accounts |
| Client isolation | Manual | Per-demo credentials |
| Duration | Always-on | Time-boxed demos |

---

## 🧪 Demo Categories (Planned)

| Category | Examples |
|---|---|
| Media | Jellyfin |
| AI | RAG pipelines |
| Optimization | OR-Tools |
| Automation | Workflow engines |
| Visualization | Interactive dashboards |

---

## ⚙️ Operational Philosophy

- Prefer boring, understandable systems
- Avoid unnecessary orchestration
- Keep UI static and cheap
- Start demos only when needed
- Everything should survive a reboot

---

## 📝 Notes

- No secrets live in this repository
- Infrastructure is managed externally
- This repo is safe to share publicly

---

## 📜 License

Private project.  
Reuse allowed for personal demos and experimentation.

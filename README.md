# Compo Capital Advisors — Production Application

A premium, high-performance, and responsive multi-page web application built to senior-development standards.

## Project Architecture

This application is structured to segregate backend logic from the public frontend distribution folder:

```
/ (Root directory)
  ├── package.json               # Root scripts to orchestrate dependencies and servers
  ├── .gitignore                 # Standard exclusions for node_modules, logs, and env configs
  ├── .env.example               # Template for backend server configuration
  ├── README.md                  # Comprehensive run and deploy documentation
  └── src/
      ├── backend/
      │   ├── server.js          # Express server with compression, helmet headers, and caching
      │   ├── package.json       # Backend dependencies (express, compression, helmet, dotenv)
      │   └── .env               # Local environment settings (gitignored)
      └── frontend/
          ├── index.html         # Homepage
          ├── about.html         # About Us
          ├── why-compo.html     # Why Compo
          ├── what-we-do.html    # What We Do
          ├── founder.html       # Our Founder
          ├── contact.html       # Contact Us
          ├── css/
          │   └── style.css      # Consolidated corporate stylesheet
          ├── js/
          │   └── main.js        # Main interaction and animation controllers
          └── images/
              ├── logo.png       # Original client transparent PNG logo
              ├── home_video.mp4 # Video Loop (NYC Skyline)
              ├── why_video.mp4  # Video Loop (Sunset Beach)
              ├── about_video.mp4# Video Loop (Oceans Waves)
              └── *.jpg          # Fallback images for mobile devices
```

---

## Senior Engineering Features

1. **Gzip / Deflate Compression**: Configured dynamically in the Express pipeline via `compression` middleware to optimize streaming speed for video loops and high-res media.
2. **Security Hardening**: Utilizes `helmet` to set secure HTTP response headers (XSS protections, Frame Options, Sniffing preventions).
3. **Advanced Asset Caching**: Serves CSS/JS and static image/video assets with long-lived `Cache-Control` max-age headers to ensure fast repeat page load speeds.
4. **Clean URLs and SPA Routing**: Routes missing extensions gracefully and points wildcard traffic to the home template.
5. **Robust Contact Form Validation**: A secure API post endpoint at `/api/contact` processes form submissions, validating inputs and sanitizing payloads.

---

## Getting Started

### Prerequisites
* [Node.js](https://nodejs.org/) (v16.0.0 or higher recommended)

### Installation
From the root of the project, install dependencies for all workspaces:
```bash
npm run install:backend
```

### Running Locally
To launch the application in development:
```bash
npm run dev
```
The server will start at **[http://localhost:8080/](http://localhost:8080/)**.

---

## Production Deployment

This project is packaged to be fully cloud-ready. You can deploy it to platforms like:
* **Google Cloud Run** (utilizing Docker or Node buildpacks)
* **Heroku / AWS Elastic Beanstalk** (pointed to the start script)
* **Linux VPS** (configured behind Nginx reverse-proxy and managed by PM2)

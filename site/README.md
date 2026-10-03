# Viridian website

Static commercial site for Viridian experimental assurance.

## Local preview

```bash
python -m http.server 8080
```

Open `http://localhost:8080` from this directory.

## Netlify

No build step is required. Set the publish directory to the repository directory containing this site (or `site` if this directory is committed under `site/` in a larger repository).

The site intentionally avoids build frameworks and third-party JavaScript. The only external runtime dependency is the IBM Plex font stylesheet served by Google Fonts.

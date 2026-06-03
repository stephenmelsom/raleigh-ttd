# Raleigh Things To Do

A simple, mobile-friendly page of our favorite restaurants, coffee shops, bakeries, and attractions around Raleigh & Cary, NC — made to share with friends and family. Every entry links to its website and a Google Maps location.

It's a dependency-free static site: just `index.html` and `style.css`, no build step.

## View it locally

Open `index.html` in any browser, or serve the folder:

```sh
python3 -m http.server
# then visit http://localhost:8000
```

## Editing the list

All content lives directly in `index.html`, grouped into five sections: **Short List**, **Restaurants**, **Coffee Shops**, **Bakeries**, and **Attractions**. To add a place, copy an existing `<article class="card">` block and update the name, city pill, description, and the two links. Map links use the form:

```
https://www.google.com/maps/search/?api=1&query=<URL-encoded "Name, Address">
```

`raw.txt` holds the original source notes (not used by the site).

## Deploying to GitHub Pages

Push this folder to a public GitHub repo, then enable **Settings → Pages → Source: Deploy from a branch → `main` / root**. The site will be served at `https://<username>.github.io/<repo>/`.

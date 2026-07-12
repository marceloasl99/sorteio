# Team Draw

A simple, mobile-friendly web application for randomly distributing participants among selected locations.

## Pages

- `index.html` — Main entry page.
- `sp.html` — São Paulo draw.
- `ma.html` — Mairiporã draw.
- `nomes.txt` — Participant list, with one name per line.

## Features

- Mobile-friendly interface.
- Quick participant and location selection.
- Balanced random distribution.
- Local weather forecast.
- Copy-ready result formatted for WhatsApp.
- No installation or database required.

## How to update the participant list

Open `nomes.txt` and enter one participant per line:

```text
Alex
Jordan
Taylor
Morgan
Casey
```

Save the file using UTF-8 encoding and keep it in the same folder as the HTML files.

## How to publish with GitHub Pages

1. Upload all project files to the repository root.
2. Open **Settings** in the GitHub repository.
3. Select **Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select the `main` branch and the `/ (root)` folder.
6. Click **Save**.

The website will then be available through the GitHub Pages address shown in the repository settings.

## Project structure

```text
/
├── index.html
├── sp.html
├── ma.html
├── nomes.txt
└── README.md
```

## Notes

- The participant file must remain in the same directory as the HTML pages.
- The application must be opened through an HTTP or HTTPS server. Loading the HTML directly through `file://` may prevent the browser from reading the participant file.
- Weather information is loaded from an external weather service and requires an internet connection.

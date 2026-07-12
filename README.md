# Team Draw

A lightweight, mobile-friendly web application that randomly distributes selected participants among selected locations.

The project runs entirely in the browser using plain HTML, CSS, and JavaScript. It does not require a database, backend service, package manager, build process, or local installation.

## Live pages

When published, the project contains the following pages:

- `index.html` — Location selection page.
- `sp.html` — São Paulo draw page.
- `ma.html` — Mairiporã draw page.

## Main features

- Responsive interface optimized for mobile phones.
- Simple participant selection.
- **Select all** and **Clear** actions.
- Clear visual difference between selected participants and selected locations.
- Random participant distribution.
- Balanced distribution among all selected locations.
- Current local weather information.
- Result date and time.
- One-click result copy.
- WhatsApp-friendly result formatting.
- No login, database, cookies, or server-side processing.

## Project structure

```text
/
├── index.html
├── sp.html
├── ma.html
├── nomes.txt
├── nomex.txt
└── README.md
```

### File descriptions

#### `index.html`

The project landing page. It allows the user to choose between the São Paulo and Mairiporã draw pages.

#### `sp.html`

The São Paulo version of the draw.

Available locations:

1. Altar
2. Frente
3. Fundo
4. Vestiário

The `Estoque` location is intentionally not included.

#### `ma.html`

The Mairiporã version of the draw.

Available locations, in priority order:

1. Amarelo
2. Verde
3. Laranja
4. Azul Claro
5. Azul Escuro

`Amarelo` appears first and therefore receives the first participant from the shuffled participant list when all locations are selected.

The `Estoque` location is intentionally not included.

#### `nomes.txt`

The active participant list used by both draw pages.

The HTML pages load this file with:

```javascript
fetch('nomes.txt')
```

For this reason, `nomes.txt` must remain in the same directory as `sp.html` and `ma.html`.

#### `nomex.txt`

An example participant list containing generic names. This file is provided only as a template and is not loaded automatically by the application.

To use the example list, copy its contents into `nomes.txt` or rename `nomex.txt` to `nomes.txt`.

#### `README.md`

Project documentation, configuration instructions, publishing steps, and troubleshooting information.

## Participant list format

Add one participant per line in `nomes.txt`:

```text
Alex
Jordan
Taylor
Morgan
Casey
```

The application automatically:

- Removes empty lines.
- Removes leading and trailing spaces.
- Ignores duplicated names.
- Preserves accented characters when the file is saved correctly.

### Character encoding

Save `nomes.txt` using **UTF-8** encoding.

This is important for names containing accented or non-ASCII characters, such as:

```text
João
José
Márcia
André
```

Avoid saving the file with legacy encodings such as ANSI or Windows-1252, because accented names may be displayed incorrectly.

## How the draw works

1. The application loads the participants from `nomes.txt`.
2. The user selects one or more participants.
3. The user selects one or more locations.
4. The application shuffles the selected participant list.
5. Participants are distributed sequentially among the selected locations.
6. If the number of participants is greater than the number of locations, distribution continues from the first selected location.
7. The result is displayed with the draw date and time.

### Distribution example

If seven participants and three locations are selected, the distribution will follow this pattern:

```text
Location 1: Participant 1, Participant 4, Participant 7
Location 2: Participant 2, Participant 5
Location 3: Participant 3, Participant 6
```

The participant order is randomized before every draw.

## Copying the result

After completing a draw, select **COPY RESULT**.

The copied text includes:

- Draw title.
- Date and time.
- Selected locations.
- Participants assigned to each location.
- Current weather information.

The result is formatted for direct pasting into WhatsApp. A typical copied result looks like this:

```text
🎯 *SORTEIO SÃO PAULO*

📅 12/07/2026 at 14:30

📍 *Altar*
• Alex
• Jordan

📍 *Frente*
• Taylor

🌤️ *WEATHER FORECAST*
Partly cloudy, 22°C now | Min. 16°C / Max. 25°C | Rain: 30%
```

The asterisks are intentional. WhatsApp uses them to display the titles in bold.

## Weather information

Each draw page displays local weather information at the bottom of the page.

The weather section includes:

- Current temperature.
- Current weather condition.
- Minimum temperature.
- Maximum temperature.
- Probability of rain.

Weather data is requested directly from the Open-Meteo API in the user's browser.

Configured locations:

- `sp.html` — São Paulo coordinates.
- `ma.html` — Mairiporã coordinates.

No API key is required by the current implementation.

An active internet connection is required to retrieve weather information. If the weather service is unavailable, the draw itself will continue to work and the page will display a weather-unavailable message.

## Running the project

The project does not require Node.js, npm, Java, Maven, Docker, or any other installation.

However, the HTML files should be served through HTTP or HTTPS because browsers may block `fetch('nomes.txt')` when a page is opened directly from the local filesystem.

### Correct access methods

```text
https://example.com/index.html
https://username.github.io/repository/
http://localhost:8000/
```

### Method that may fail

```text
file:///C:/project/index.html
```

If the page displays `Error loading nomes.txt`, verify that the project is being accessed through a web server and that `nomes.txt` is in the repository root.

## Publishing with GitHub Pages

### 1. Upload the files

Upload these files to the root of the GitHub repository:

```text
index.html
sp.html
ma.html
nomes.txt
nomex.txt
README.md
```

Do not place the HTML files or `nomes.txt` inside another folder unless the paths inside the HTML files are also updated.

### 2. Commit the files

Use a clear commit message, for example:

```text
Publish updated team draw application
```

Commit the files directly to the `main` branch.

### 3. Enable GitHub Pages

In the repository:

1. Open **Settings**.
2. Select **Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select the `main` branch.
5. Select the `/ (root)` folder.
6. Select **Save**.

After deployment, the pages will normally be available at:

```text
https://USERNAME.github.io/REPOSITORY/
https://USERNAME.github.io/REPOSITORY/sp.html
https://USERNAME.github.io/REPOSITORY/ma.html
```

Replace `USERNAME` and `REPOSITORY` with the GitHub account and repository names.

## Publishing on another web host

The project can also be published on any static hosting service or traditional web server.

Upload all files to the same public directory, for example:

```text
public_html/
├── index.html
├── sp.html
├── ma.html
├── nomes.txt
├── nomex.txt
└── README.md
```

No PHP, database, or server-side configuration is required.

## Updating the application

### Update participants

Edit only `nomes.txt`, keeping one participant per line.

### Update São Paulo locations

Open `sp.html` and edit the checkboxes inside the locations section. Each location requires:

- A unique `id`.
- The `name="local"` attribute.
- A `value` containing the location name.
- A matching `label` using the same `id` in the `for` attribute.

### Update Mairiporã location priority

The location order in `ma.html` defines the distribution order after the participant list is shuffled.

To change the priority, move the complete location block to the desired position. The first selected location receives the first shuffled participant.

### Update weather coordinates

Each page contains an Open-Meteo request with latitude and longitude parameters.

Update both values when changing the city:

```text
latitude=YOUR_LATITUDE
longitude=YOUR_LONGITUDE
```

Also verify that the timezone remains appropriate for the selected location.

## Troubleshooting

### Participants do not load

Check the following:

- The active file is named exactly `nomes.txt`.
- File names use the correct uppercase and lowercase letters.
- `nomes.txt` is in the same directory as `sp.html` and `ma.html`.
- The page is accessed using HTTP or HTTPS.
- The hosting service serves `.txt` files.
- The browser is not displaying an old cached version.

### Accented names are displayed incorrectly

Save `nomes.txt` using UTF-8 encoding and upload it again.

### The latest version is not visible

Try the following:

1. Confirm that the new files were committed to the branch used by GitHub Pages.
2. Check **Settings → Pages** and verify the selected branch and folder.
3. Wait for the GitHub Pages deployment to finish.
4. Refresh the page without cache.
5. Open the site in a private browser window.

### Weather information does not load

Check the following:

- The device has internet access.
- The browser allows requests to the weather API.
- The weather service is available.
- The latitude, longitude, and timezone are valid.

The draw remains available even if weather information cannot be retrieved.

### The copy button does not work

Clipboard access may be restricted by the browser when the page is not served through HTTPS.

Use the published HTTPS website and allow clipboard access if the browser requests permission. The application also includes a legacy copy fallback for compatible browsers.

### GitHub Pages returns a 404 error

Verify that:

- `index.html` exists in the published root directory.
- GitHub Pages is enabled.
- The correct branch is selected.
- The `/ (root)` folder is selected.
- The deployment workflow has completed successfully.

## Browser compatibility

The application is designed for current versions of:

- Google Chrome.
- Microsoft Edge.
- Mozilla Firefox.
- Apple Safari.
- Android mobile browsers.
- iOS mobile browsers.

For the best clipboard and network behavior, use the application through HTTPS.

## Privacy

Participant selection and draw processing occur locally in the browser.

The application does not include:

- User accounts.
- Authentication.
- A database.
- Analytics.
- Tracking cookies.
- Server-side participant storage.

Participant names are stored only in the static `nomes.txt` file published with the project. Weather requests are sent to the configured external weather service.

## Security considerations

- Do not store passwords, personal documents, confidential information, or sensitive personal data in `nomes.txt`.
- Remember that files in a public GitHub repository and public website can be viewed by anyone.
- Use only the minimum participant information required for the draw.
- Review the participant list before publishing changes.

## License

No license is currently defined. Add a `LICENSE` file if the project will be distributed, reused, or maintained by other contributors.

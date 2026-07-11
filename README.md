# Quran Verse Finder

A simple, responsive web application for looking up individual Quran verses by surah and ayah number.

Users can enter a reference such as `2/72` or `2:72` to view:

- The Quran verse in Arabic Uthmani script
- The Saheeh International English translation
- The surah number and English name
- The surah name in Arabic
- The ayah number

## Live Demo

[Open Quran Verse Finder](https://alirafique026.github.io/Quran/)

## Features

- Search by Quran reference using either `surah/ayah` or `surah:ayah`
- Displays Arabic text in a right-to-left layout
- Displays an English translation beneath the Arabic verse
- Supports keyboard search by pressing **Enter**
- Validates the reference format and surah number
- Shows loading and error messages
- Responsive design suitable for desktop and mobile browsers
- No installation, framework, or build process required

## Example

Enter:

```text
2/255
```

or:

```text
2:255
```

The application retrieves and displays Surah Al-Baqarah, Ayah 255.

## How It Works

The application normalizes the user's input by converting `/` to `:` and checks that it follows this pattern:

```text
surah:ayah
```

It then sends two requests to the [Al Quran Cloud API](https://alquran.cloud/api):

```javascript
const arabicUrl =
  `https://api.alquran.cloud/v1/ayah/${surah}:${ayah}/quran-uthmani`;

const englishUrl =
  `https://api.alquran.cloud/v1/ayah/${surah}:${ayah}/en.sahih`;
```

Both requests are made at the same time using `Promise.all()`:

```javascript
const [arabicRes, englishRes] = await Promise.all([
  fetch(arabicUrl),
  fetch(englishUrl)
]);
```

The returned JSON data is then used to display the Arabic verse, English translation, surah names, and ayah number.

## Technologies Used

- HTML5
- CSS3
- Vanilla JavaScript
- Fetch API
- Al Quran Cloud API
- GitHub Pages

## Project Structure

```text
Quran/
├── index.html
└── README.md
```

The complete application is currently contained in `index.html`, including its markup, styling, and JavaScript.

## Run Locally

Because this is a static web application, no package installation is required.

### Option 1: Open the file directly

1. Clone the repository:

   ```bash
   git clone https://github.com/alirafique026/Quran.git
   ```

2. Open the project folder:

   ```bash
   cd Quran
   ```

3. Open `index.html` in a web browser.

### Option 2: Use a local web server

Using Python:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

## Input Validation

The application currently checks that:

- The input is not empty
- The reference contains a surah and ayah number
- The format resembles `2/72` or `2:72`
- The surah number is between 1 and 114
- The requested verse exists in the API

If the reference is invalid or the API request fails, the application displays an error message.

## API Editions

The application currently uses:

| Content | API edition |
|---|---|
| Arabic Quran text | `quran-uthmani` |
| English translation | `en.sahih` |

The English edition can be changed by replacing `en.sahih` with another translation identifier supported by the Al Quran Cloud API.

## Deployment

The project is deployed with GitHub Pages from this repository:

[https://github.com/alirafique026/Quran](https://github.com/alirafique026/Quran)

Live site:

[https://alirafique026.github.io/Quran/](https://alirafique026.github.io/Quran/)

## Possible Future Improvements

- Add a translation selector
- Add a surah dropdown and ayah dropdown
- Include audio recitation
- Add previous and next ayah buttons
- Allow users to copy or share a verse
- Add dark mode
- Save recently viewed verses
- Add more detailed validation for ayah ranges
- Improve accessibility with ARIA labels and status announcements

## Disclaimer

This application retrieves Quran text and translations from a third-party API. Users should refer to verified Quran publications and qualified scholars when accuracy, interpretation, or religious rulings are important.

## Author

**Mohammad Ali Rafique**

- GitHub: [@alirafique026](https://github.com/alirafique026)
- Live project: [Quran Verse Finder](https://alirafique026.github.io/Quran/)

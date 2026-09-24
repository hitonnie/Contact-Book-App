Contact Book App

A contact management app from FNB Week 6, the first project in the series to connect to a real backend API rather than using static or hardcoded data. It fetches and displays contacts from a remote REST API, gated behind a simple API key flow.

How It Works
On load, config.js checks localStorage for a saved apiKey.
If no key is found, the user is redirected to enter-api-key.html, where they submit a key that's validated against the API (GET /controller/api-key/?apiKey=...).
Once validated, the key is stored in localStorage and the user is redirected to index.html.
index.html calls fetchContacts() on page load, which requests GET /controller/get-contacts/, then renders each contact's avatar, first name, and last name into a table.
A Refresh button re-fetches the contact list on demand.
API
Base URL: https://mysite.itvarsity.org/api/ContactBook/
Endpoints used:
controller/api-key/?apiKey=<key> — validates an API key (returns "1" on success)
controller/get-contacts/ — returns the contact list as JSON
controller/uploads/<avatar> — serves contact avatar images
Project Structure
Contact-Book-App/
├── index.html            # Main contact list view
├── enter-api-key.html    # API key entry / validation screen
├── config.js              # Shared API key check + root path constant
└── README.md
How to Run

No build tools required, but you do need a valid API key for mysite.itvarsity.org.

Clone the repository:
bash
   git clone https://github.com/hitonnie/Contact-Book-App.git
Open index.html in your browser (or enter-api-key.html directly).
If prompted, enter a valid API key. It's saved in localStorage so you won't need to re-enter it on future visits from the same browser.
Built With
HTML5
Vanilla JavaScript (fetch, localStorage, template literals)
A remote REST API (ContactBook API on itvarsity.org)
Known Issues
"Add Contact" button has no handler — the button exists in index.html but there's no corresponding event listener or function, so clicking it currently does nothing.
Possible double-slash in fetch URL — rootPath already ends in / (.../ContactBook/), and fetchContacts() appends another leading / ("/controller/get-contacts/"), which can produce a doubled // in the final URL depending on how the server handles it.
API key stored in plain localStorage — fine for a learning exercise, but not a pattern to carry into anything handling real user credentials.
Context

Built as part of Week 6 coursework, this project introduces working with a real external API: fetching JSON data, handling asynchronous responses, and gating access behind a stored credential.

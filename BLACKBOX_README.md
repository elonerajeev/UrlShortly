 ```
# URL Shortener

This is a simple URL shortener that allows users to shorten long URLs. The short URLs are generated using a random string of characters.

## How to use

To use the URL shortener, simply enter a long URL into the text field and click the "Shorten URL" button. The short URL will then be displayed on the page.

## Code

The code for the URL shortener is written in HTML, CSS, and JavaScript. The HTML code creates the user interface, the CSS code styles the user interface, and the JavaScript code handles the logic of the URL shortener.

The following code snippets show the key parts of the code:

```html
<form id="urlShortenerForm">
  <label for="longUrl">Enter a long URL:</label>
  <input type="text" id="longUrl" name="longUrl" required>
  <button type="submit">Shorten URL</button>
</form>

<p>Shortened URL: <span id="shortUrl"></span></p>
<p id="error"></p>
```

The HTML code creates a form with a text field and a submit button. The text field is used to enter the long URL, and the submit button is used to trigger the URL shortening process.

The following JavaScript code handles the logic of the URL shortener:

```javascript
document.getElementById('urlShortenerForm').addEventListener('submit', function (e) {
  e.preventDefault();
  const longUrl = document.getElementById('longUrl').value;
  const errorElement = document.getElementById('error');
  errorElement.textContent = ''; // Clear any previous error message

  fetch('/shorten', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({ longUrl }),
  })
    .then(response => {
      if (!response.ok) {
        throw new Error('Error shortening URL');
      }
      return response.json();
    })
    .then(data => {
      const shortUrl = data.shortUrl;
      document.getElementById('shortUrl').textContent = shortUrl;
    })
    .catch(error => {
      console.error('Error:', error);
      errorElement.textContent = 'An
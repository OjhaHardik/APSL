# Allenhouse Admissions 2027-28 landing page

Plain HTML, CSS and JavaScript. No build step, no framework.

```
index.html            the page
css/styles.css        all styles (mobile-first, responsive)
js/main.js            mobile menu + enquiry form validation/submit
submit.php            saves each enquiry as a row in data/enquiries.csv
data/enquiries.csv    the enquiry records (open in Excel / Google Sheets)
data/.htaccess        blocks public download of the CSV
.htaccess             index.html as default page, no folder listings
assets/img/           logo and hero photo
dev-server.js         local testing only (Node); do not upload
_design-reference/    the original design-tool export; do not upload
```

## Hosting

1. Upload everything except `dev-server.js` and `_design-reference/` to a host with
   PHP 7.2 or newer (any cPanel / Hostinger / Apache / LiteSpeed shared hosting works).
2. Make sure `data/` is writable by the web server (permissions 755, or 775 if saving fails).
3. Download the records any time from the hosting file manager: `data/enquiries.csv`.
   The CSV cannot be opened from the browser; that is intentional.

On Nginx hosting, `.htaccess` is ignored. Add this to the server block instead:

```
location ^~ /data/ { deny all; }
```

On static-only hosting (GitHub Pages, Netlify without functions) PHP does not run,
so the form shows its error message. Point `FORM_ENDPOINT` at the top of
`js/main.js` to a working endpoint in that case.

## Local testing

The form needs PHP, so VS Code Live Server and opening the file directly will
always show "Sorry, we couldn't send your enquiry". Use one of these instead:

- **XAMPP:** `C:\xampp\htdocs\APSL` is linked to this folder. Start Apache and open
  http://localhost/APSL/
- **Node:** run `node dev-server.js` and open http://localhost:5502
  (stop Live Server first, it uses the same port).

Submissions are written to `data/enquiries.csv`.

## Still to do before going live

- `privacy.html` is linked from the form and footer but does not exist yet.
  Add it, or change both links to the school's existing privacy page.

# Berry Vibes Restaurant API Worker 🍓

This folder is the **private-key bridge** between the public GitHub Pages website and a nutrition provider.

## 1. Create a Cloudflare Worker
Create a Worker named something like `berry-restaurant-api` and paste in `restaurant-worker.js`.

## 2. Add Worker secrets
Add these as Cloudflare Worker secrets/environment secrets:

- `NUTRITIONIX_APP_ID`
- `NUTRITIONIX_APP_KEY`

Never paste either value into GitHub, `config.js`, `script.js`, or an HTML file.

## 3. Restrict browser access to your GitHub Pages origin
Add a normal Worker variable:

`ALLOWED_ORIGIN=https://YOUR-GITHUB-USERNAME.github.io`

If your Pages site uses a custom domain, use that origin instead.

## 4. Deploy and test
After deployment, open:

`https://YOUR-WORKER.workers.dev/health`

You should get JSON similar to:

```json
{"ok":true,"service":"berry-restaurant-api"}
```

Then test a lookup:

`https://YOUR-WORKER.workers.dev/?restaurant=Wendys&item=Baconator`

## 5. Connect Berry Vibes
Open the website root `config.js` and paste the public Worker URL:

```js
window.BERRY_RESTAURANT_ENDPOINT =
  "https://YOUR-WORKER.workers.dev/";
```

The website now checks in this order:

1. Built-in Berry Vibes restaurant vault
2. Your personal saved restaurant foods in localStorage
3. Cloudflare Worker nutrition lookup
4. Optional “Save to My Vault” so repeat searches do not need the API

## Accuracy note
Restaurant nutrition can change and customizations can alter nutrition. Berry Vibes labels the source and does not fabricate missing values.

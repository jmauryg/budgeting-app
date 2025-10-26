# My Budgeting App — GitHub Pages

This repository hosts a minimal public site required by some OAuth institutions when using Plaid.
The budgeting application itself runs locally.

## URLs you will use
- **Website URL (Plaid Dashboard)**: `https://<your-username>.github.io/my-budgeting-app/`
- **Redirect URI (Plaid Dashboard + link_token.create)**: `https://<your-username>.github.io/my-budgeting-app/plaid/oauth-return.html`

> Replace `<your-username>` with your GitHub username. If you choose a different repository name,
> update the path accordingly.

## Local callback
The OAuth return page forwards the full query string to your local app:

```
http://localhost:3000/plaid/oauth/callback?<original Plaid query params>
```

If your local callback differs, edit `plaid/oauth-return.html` and change `LOCAL_CALLBACK`.

## Example (Node) link_token
```js
const linkTokenRes = await plaid.linkTokenCreate({
  user: { client_user_id: userId },
  client_name: "My Budgeting App",
  products: ["transactions"],
  country_codes: ["US"],
  language: "en",
  redirect_uri: "https://<your-username>.github.io/my-budgeting-app/plaid/oauth-return.html"
});
```

## Enable GitHub Pages
1. Push these files to your repo (e.g., `my-budgeting-app`).
2. Settings → Pages → “Deploy from a branch” → `main` / `/ (root)`.
3. Wait for the Pages URL to appear; then paste it into the Plaid Dashboard (Website URL).
4. Add the exact Redirect URI above to Plaid's allowed redirect URIs and pass it in `link_token.create`.

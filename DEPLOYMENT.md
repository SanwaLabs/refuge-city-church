# Deployment

This site is hosted for free with GitHub Pages from:

https://github.com/SanwaLabs/refuge-city-church

Live site:

https://sanwalabs.github.io/refuge-city-church/

## Update The Site

After editing files locally, deploy updates with:

```sh
git add .
git commit -m "Update site"
git push
```

GitHub Pages will rebuild automatically after each push to `main`.

## GitHub Pages Settings

In the GitHub repo, go to `Settings` > `Pages`.

Use these settings:

- Source: `Deploy from a branch`
- Branch: `main`
- Folder: `/ root`

The repo must remain public for free GitHub Pages hosting on GitHub Free for organizations.

## Namecheap Custom Domain

When you are ready to connect the real domain, add a `CNAME` file to this repo containing the root domain, for example:

```text
example.com
```

Then in Namecheap, go to `Domain List` > `Manage` > `Advanced DNS` and add these records.

Root domain records:

```text
Type: A Record
Host: @
Value: 185.199.108.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.109.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.110.153
TTL: Automatic

Type: A Record
Host: @
Value: 185.199.111.153
TTL: Automatic
```

WWW record:

```text
Type: CNAME Record
Host: www
Value: sanwalabs.github.io
TTL: Automatic
```

After DNS updates finish propagating, go back to GitHub `Settings` > `Pages`, enter the custom domain, save it, and enable `Enforce HTTPS`.

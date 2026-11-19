# Material Requirement Processing (MRP) Desk

A browser-based academic prototype for planning production, exploding a Bill of Materials (BOM), comparing material demand with available stock, and reviewing purchase requirements.

> **Academic demo only.** Product, plan, material, and stock values are illustrative sample data. This prototype is not intended for real manufacturing or purchasing decisions.

## What it demonstrates

- **Overview dashboard** — summarizes sample products, materials, planned production, demand versus stock, and material shortages.
- **Production planning** — create and review illustrative production plans, then preview the material requirements for a batch.
- **Product and material catalogues** — add, edit, and remove finished products and raw materials, including their codes, units, and stock values.
- **Bill of Materials** — connect finished products to the materials and quantities needed per unit.
- **Purchase-needs report** — aggregate gross demand across open plans, apply current stock once per material, and export positive net needs as CSV. It does not create or send purchase orders.

## MRP calculation

For each material, the prototype calculates:

```text
Gross requirement = planned production quantity × BOM quantity per finished unit
Net requirement   = max(0, gross requirement − available stock)
```

The purchase-needs page aggregates gross requirements across open plans before applying stock once. Each material retains its own unit; unrelated units are not combined.

## Demo sign-in and data storage

The opening sign-in screen is a **visual demo gate, not authentication or security**. Any syntactically valid email address and any non-empty password will open the workspace. The application does not validate, transmit, or store the password. It keeps the email in the current browser tab’s session storage. The gate can be bypassed and does not protect the website or its data.

MRP sample records and edits are stored in the browser’s local storage on that device. There is no backend, shared database, user-account system, or synchronization between users or devices.

## Technology

- HTML
- CSS
- Vanilla JavaScript
- Browser `localStorage` for MRP demo records and `sessionStorage` for the temporary demo identity

No package installation or build step is required for the static prototype.

## Run locally

With Python 3 installed, run this command from the project folder:

```sh
python3 -m http.server 3000 --directory public
```

Open [http://localhost:3000](http://localhost:3000) in your browser. Serving the `public/` directory is important because the site loads its styles and scripts from the site root.

## Project files

```text
README.md             Project overview and run instructions
TODO.md               Feature checklist
app.config.ts         Manus Webdev project metadata
public/
  index.html           Sign-in screen and application shell
  app.css              Responsive interface styles
  app.js               MRP calculations, demo sign-in gate, and interactions
  logo.svg             Site mark
  favicon.svg          Browser icon
  manus-routes.json    Webdev route manifest
```

`app.config.ts` is metadata for the Manus Webdev environment and is not needed by a basic static host.

## Add this project to the existing GitHub repository

Repository provided: <https://github.com/ArkaSK123/material-requirement.git>

To preserve the repository’s existing history and files, clone it first, then copy the project files from the ZIP into that clone. From the cloned repository folder, review the changes and push normally:

```sh
git status
git add README.md TODO.md app.config.ts public
git commit -m "Add MRP Desk website"
git push
```

Do not run `git init` over an existing clone or force-push. If your repository already contains a README or other files, keep them and merge the project files rather than replacing the repository contents.

### GitHub Pages note

The website currently uses root-relative asset paths such as `/app.css` and `/app.js`. For a GitHub Pages **project site** hosted under a repository subpath (for example, `/material-requirement/`), change those paths to relative paths before deployment. A custom-domain or account-level site served from the root does not have this subpath issue.

# ddev-craftcms-vite 

Simple demo repository for CraftCMS + DDEV, including support for [nystudio107/craft-vite](https://github.com/nystudio107/craft-vite).

- Status: 🚧 Work in progress 🚧
- Local URL: https://ddev-craftcms-vite.ddev.site/

## Local setup (after clone)

```bash
ddev start
ddev composer install
ddev craft install
ddev npm install
ddev craft plugin/install vite

# Open your website, 
ddev launch
# run local dev server (vite),
ddev npm run dev
# and hit reload
```

## How was this created?

1. Followed the official [DDEV Quickstart for CraftCMS](https://ddev.readthedocs.io/en/latest/users/quickstart/#craft-cms)

```bash
# https://ddev.readthedocs.io/en/latest/users/quickstart/#craft-cms
# Create a project directory and move into it:
mkdir my-craft-project
cd my-craft-project

# Set up the DDEV environment:
ddev config --project-type=craftcms --docroot=web --create-docroot

# Boot the project and install the starter project:
ddev start
ddev composer create -y --no-scripts craftcms/craft

# Run the Craft installer:
ddev craft install
ddev launch
```

2. Installed [nystudio107/craft-vite](https://github.com/nystudio107/craft-vite):

```bash
# install via composer
ddev composer require nystudio107/craft-vite
# activate within craftcms
ddev craft plugin/install vite
```

3. Exposing the ports via [web_extra_exposed_ports](https://ddev.readthedocs.io/en/latest/users/extend/customization-extendibility/#exposing-extra-ports-via-ddev-router):

```yaml
web_extra_exposed_ports:
  - name: craft-vite
    container_port: 3000
    http_port: 2999
    https_port: 3000
```

⚠️ `ddev restart` is needed afterwards

4. Following https://nystudio107.com/docs/vite/#using-ddev and extend the previous config of `vite.config.js`:

```javascript
/* vite.config.js */
server: {
  host: '0.0.0.0',
  port: 3000
}
```

5. Install npm deps, as stated here: https://nystudio107.com/blog/using-vite-js-next-generation-frontend-tooling-with-craft-cms

```bash
ddev npm init -y
ddev npm install -D vite vite-plugin-restart postcss autoprefixer @vitejs/plugin-legacy sass
```

Add the following scripts to `package.json`:

```json
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

- [ ] TODO: Is @vitejs/plugin-legacy always needed? (https://nystudio107.com/blog/using-vite-js-next-generation-frontend-tooling-with-craft-cms)

6. Edited `index.twig`, added craft-vite (and created `app.js` + `app.scss` file)

```
    {{ craft.vite.script("src/js/app.js") }} 
```

7. That's it, have fun!

## Further resources

- https://nystudio107.com/blog/using-vite-js-next-generation-frontend-tooling-with-craft-cms
- https://github.com/szenario-fordesigners/craft-vite-starter / https://twitter.com/thomasbendl/status/1628741476355112962
- More experiments and info about DDEV + vite: https://my-ddev-lab.mandrasch.eu/

Connect with the DDEV community on [Discord](https://discord.gg/hCZFfAMc5k)

Thanks to the DDEV maintainers and DDEV open source community! 💚

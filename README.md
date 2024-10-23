<p align="center">
  <img src="https://raw.githubusercontent.com/bitwarden/brand/main/screenshots/apps-combo-logo.png" alt="Bitwarden" />
</p>
<p align="center">
  <a href="https://github.com/bitwarden/clients/actions/workflows/build-browser.yml?query=branch:main" target="_blank"><img src="https://github.com/bitwarden/clients/actions/workflows/build-browser.yml/badge.svg?branch=main" alt="GitHub Workflow browser build on main" /></a>
  <a href="https://github.com/bitwarden/clients/actions/workflows/build-cli.yml?query=branch:main" target="_blank"><img src="https://github.com/bitwarden/clients/actions/workflows/build-cli.yml/badge.svg?branch=main" alt="GitHub Workflow CLI build on main" /></a>
  <a href="https://github.com/bitwarden/clients/actions/workflows/build-desktop.yml?query=branch:main" target="_blank"><img src="https://github.com/bitwarden/clients/actions/workflows/build-desktop.yml/badge.svg?branch=main" alt="GitHub Workflow desktop build on main" /></a>
  <a href="https://github.com/bitwarden/clients/actions/workflows/build-web.yml?query=branch:main" target="_blank"><img src="https://github.com/bitwarden/clients/actions/workflows/build-web.yml/badge.svg?branch=main" alt="GitHub Workflow web build on main" /></a>
  <a href="https://gitter.im/bitwarden/Lobby" target="_blank"><img src="https://badges.gitter.im/bitwarden/Lobby.svg" alt="gitter chat" /></a>
</p>

---

# Bitwarden Client Applications

This repository houses all Bitwarden client applications except the [Mobile application](https://github.com/bitwarden/mobile).

Please refer to the [Clients section](https://contributing.bitwarden.com/getting-started/clients/) of the [Contributing Documentation](https://contributing.bitwarden.com/) for build instructions, recommended tooling, code style tips, and lots of other great information to get you started.

## Build Stuff

[Bitwarden is no longer free software (HN)](https://news.ycombinator.com/item?id=41893994)

### Set up environment: `.github/workflows/build-desktop.yml#155`

- `sudo apt-get -y install pkg-config libxss-dev libglib2.0-dev libsecret-1-dev rpm musl-dev musl-tools`

### Build Setup:

https://github.com/kagiko/contributing-docs/blob/main/docs/getting-started/clients/index.md

- `cd client` # root
- `nvm use 20.18.0`
- `npm ci`
- `git config blame.ignoreRevsFile .git-blame-ignore-revs`

### Build Native Module: `.github/workflows/build-desktop.yml#185`

- `cd apps/desktop/desktop_native`
- `rustup target add x86_64-unknown-linux-musl`
- `export PKG_CONFIG_ALL_STATIC=1` # these are required to compile musl builds on a GNU system
- `export PKG_CONFIG_ALLOW_CROSS=1`
- `export TARGET=musl`
- `node build.js cross-platform`

### Run

You may need to run `npm run electron` before chown/chmod on the chrome-sandbox will be available?

- `sudo chown root:root /home/steven/work/kagiko/clients/node_modules/electron/dist/chrome-sandbox`
- `sudo chmod 4755 /home/steven/work/kagiko/clients/node_modules/electron/dist/chrome-sandbox`
- `cd apps/desktop`
- `npm run electron`

### Ignore all this

- `cd apps/desktop/desktop_native/napi`
- `RUSTFLAGS="-C target-feature=-crt-static" cargo build --release --target=x86_64-unknown-linux-musl`
- `cd apps/desktop/desktop_native`
- `npm run build -- --target x86_64-unknown-linux-musl`
- `npm run build -- --target desktop-napi-linux-x64-musl` ? nope

## Related projects:

- [bitwarden/server](https://github.com/bitwarden/server): The core infrastructure backend (API, database, Docker, etc).
- [bitwarden/mobile](https://github.com/bitwarden/mobile): The mobile app vault (iOS and Android).
- [bitwarden/directory-connector](https://github.com/bitwarden/directory-connector): A tool for syncing a directory (AD, LDAP, Azure, G Suite, Okta) to an organization.

# We're Hiring!

Interested in contributing in a big way? Consider joining our team! We're hiring for many positions. Please take a look at our [Careers page](https://bitwarden.com/careers/) to see what opportunities are [currently open](https://bitwarden.com/careers/#open-positions) as well as what it's like to work at Bitwarden.

# Contribute

Code contributions are welcome! Please commit any pull requests against the `main` branch. Learn more about how to contribute by reading the [Contributing Guidelines](https://contributing.bitwarden.com/contributing/). Check out the [Contributing Documentation](https://contributing.bitwarden.com/) for how to get started with your first contribution.

Security audits and feedback are welcome. Please open an issue or email us privately if the report is sensitive in nature. You can read our security policy in the [`SECURITY.md`](SECURITY.md) file.

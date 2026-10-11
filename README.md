# Tether Homebrew tap

[Tether](https://tether.ahabyte.com) puts your dev machine in your pocket: browse files, run terminals, check git, preview dev servers and test APIs on your computer from your phone.

## Install

```sh
brew install Nirmitee-tech/tap/tether
tether start
```

On a new machine, `tether start` first asks how to run it:

- **Self-host** (the default, press Enter): everything stays on the machine, including its account. Tether opens a free Cloudflare tunnel and prints a link and a QR code; the link changes when Tether restarts. Open it on your phone and create the machine's account with the setup code it shows.
- **Tether host**: the machine joins your Tether account and gets a fixed address that never changes. The terminal shows a pairing link and a QR code; sign in to your Tether account (or create one) and approve the machine.

`tether start --self-host` or `tether start --hosted` skips the question. Either way Tether runs in the background: it restarts if it crashes and starts again at login.

| Command | |
|---|---|
| `tether start [--self-host \| --hosted]` | start in the background and print the link |
| `tether status` | is it running and reachable? |
| `tether url` | print the link |
| `tether open` | open the Tether app for this machine |
| `tether setup-code` | the one-time code for a self-hosted machine's account |
| `tether logs -f` | follow the log |
| `tether stop` | stop it (and don't start at login) |

After `brew upgrade tether`, run `tether restart`.

Works on macOS (launchd) and Linux (systemd user service). On a Linux server, run `loginctl enable-linger $USER` so it keeps running when you're logged out.

## Uninstall

On Tether host, first remove the machine from your Tether account (in the app: Settings → Remove … from your account), so its address is freed.

```sh
tether stop
brew uninstall tether
rm -rf ~/.tether     # this machine's account, projects, API collections and saved terminals
```

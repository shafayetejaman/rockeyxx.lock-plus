# Lock Plus

An Omarchy lock screen with a live clock, the date, and shutdown/reboot buttons —
built on top of Omarchy's stock lock plugin, so the password and fingerprint PAM
flows are unchanged.

## What it adds

Compared to the built-in `omarchy.lock`:

- **Live clock and date** above the password field, updating every second (`HH:mm` and `dddd, MMMM d`).
- **Shutdown and Reboot buttons** anchored to the bottom of the lock screen, with hover states themed from your active Omarchy colors.

Everything else — the password field, the separate fingerprint PAM flow, failure
handling, and theming — is Omarchy's, untouched.

## Requirements

- Omarchy 4.x (Quattro shell / Quickshell plugin system)
- No external dependencies. `systemctl poweroff` and `systemctl reboot` are called
  directly for the power buttons.

## Install

```bash
omarchy plugin add https://github.com/ommmar310-cmd/omarchy-plugin-lock-plus --enable
omarchy plugin disable omarchy.lock
```

`omarchy.lock` must be disabled — running both lock services at once means two
lock surfaces competing for the same session.

Restart the shell (or log out and back in) to pick up the change, then test with
your lock keybind before relying on it.

## Uninstall

```bash
omarchy plugin enable omarchy.lock
omarchy plugin remove rockeyxx.lock-plus
```

This restores the stock lock screen. The plugin writes nothing outside its own
folder and does not modify your `shell.json` beyond the enable/disable entries
that `omarchy plugin` manages itself.

## Updating

```bash
omarchy plugin update rockeyxx.lock-plus
```

## Security note

This is a lock screen: it is the thing standing between a locked session and your
desktop. The authentication path is inherited verbatim from Omarchy's plugin and
has not been modified — but read `LockView.qml` and `Service.qml` yourself before
installing. Omarchy plugins run unsandboxed.

## License

MIT. This is a derivative work of the Omarchy lock plugin by David Heinemeier
Hansson (https://github.com/basecamp/omarchy), redistributed under the MIT
License. See [LICENSE](LICENSE) for the full notice.

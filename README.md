# Power for the Omarchy bar, desktops included

The stock Omarchy power widget is built for laptops: without a battery it
hides itself, so a desktop cannot reach the power-profile picker at all. This
version keeps it usable without a battery.

## Changes from stock

- **Always on the bar.** With a battery it behaves exactly like the stock
  widget (charge icon, percentage on right click, battery details in the
  panel). Without one, the icon shows the active power profile and the panel
  offers only the profile picker.
- **The profile icon is right from the start.** The active profile is read at
  startup and followed through power-profiles-daemon, so changing it anywhere
  (menu, keybinding, `powerprofilesctl`) updates the icon immediately — not
  only after the panel has been opened once.

## Install

```sh
omarchy plugin add https://github.com/yesm1ke/omarchy-plugin-power --enable
omarchy plugin disable omarchy.power   # the stock widget it replaces
```

IPC keeps the stock target name: `omarchy-shell omarchy.power toggle`.

## Staying current with Omarchy

This is a copy of the stock widget with changes on top, so it would not pick
up Omarchy's own fixes by itself. The repository keeps them apart:

- branch `upstream` holds the stock files exactly as Omarchy ships them, one
  commit per Omarchy version that changed them;
- branch `main` is `upstream` plus the changes described above.

After an Omarchy update, run `./sync-upstream` in the installed plugin
(`~/.config/omarchy/plugins/<id>/`). It records the installed stock files on
`upstream` and merges them into `main`; on a conflict it aborts the merge and
leaves everything as it was, to be resolved with `git merge upstream`.
`./sync-upstream --check` only reports whether anything changed. It can be run
automatically from an Omarchy `post-update` hook.

## License

MIT, see [LICENSE](LICENSE). Based on the Omarchy power widget, © David
Heinemeier Hansson, MIT.

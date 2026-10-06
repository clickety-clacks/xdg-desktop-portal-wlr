# xdg-desktop-portal-wlr

## Contributions: AI-written submissions are welcome

AI-written submissions are welcome here. Every submission is adversarially reviewed before it is
accepted. Too many AI-written submissions that fail that review may result in a ban on having
your submissions accepted.

## This fork

This is the [Gooarchy](https://github.com/clickety-clacks/gooarchy) project's fork of
[emersion/xdg-desktop-portal-wlr](https://github.com/emersion/xdg-desktop-portal-wlr).
xdg-desktop-portal-wlr is the work of its upstream authors and keeps their MIT license
([LICENSE](LICENSE)), unchanged. The fork's changes are on the `gooarchy` branch, on top of an
upstream release; its releases are tagged `v<upstream version>-gooarchy.<n>`.

Changes from upstream 0.8.4:

- screencast: keep an in-flight capture across a pause. A consumer that pauses the stream while
  a capture is in flight (GStreamer does this while starting) no longer gets an
  ext-image-copy-capture `duplicate_frame` protocol error, which ended the stream, or a stream
  frozen after its first frame.
- screencast: don't destroy the process retry timer twice. Closing a session while the stream
  was starved of buffers crashed the portal.

The rest of this README is upstream's.

---

[xdg-desktop-portal] backend for wlroots.

Currently it only implements the following portals only and is meant to offload the missing portals to other implementations depending on the user preferences.

- org.freedesktop.impl.portal.Screenshot
- org.freedesktop.impl.portal.ScreenCast

Other portals that can be used include `gtk` for many implementations, `gnome-keyring` for the Secret portal.

## Building

```sh
meson build
ninja -C build
```

## Installing

### From Source

```sh
ninja -C build install
```

### Distro Packages

[![Packaging status](https://repology.org/badge/vertical-allrepos/xdg-desktop-portal-wlr.svg?exclude_unsupported=1)](https://repology.org/project/xdg-desktop-portal-wlr/versions)

## Running

Make sure `XDG_CURRENT_DESKTOP` is set. Make sure `WAYLAND_DISPLAY` and
`XDG_CURRENT_DESKTOP` are imported into D-Bus. If you're running Sway, this
can be added to your config file:

    exec dbus-update-activation-environment --systemd WAYLAND_DISPLAY XDG_CURRENT_DESKTOP=sway

When correctly installed, xdg-desktop-portal should automatically invoke
xdg-desktop-portal-wlr when needed.

[Recent changes](https://www.bassi.io/articles/2023/05/29/configuring-portals/) to xdg-desktop-portal is requiring desktop environments to set up a `*-portals.conf` configuration that specify which portals should be used for a given `XDG_CURRENT_DESKTOP` value. If this file does not exists in `/usr/share/xdg-desktop-portal/`, you should create it under `~/.config/xdg-desktop-portal/` with content like this:

```ini
[preferred]
default=gtk
org.freedesktop.impl.portal.Screenshot=wlr
org.freedesktop.impl.portal.ScreenCast=wlr
```

(you can specify the default portal to use for any implementation not explicitly defined, and you can add any portal you need for other specific interfaces like gnome-keyring for the Secret portal).

### Configuration

See `man 5 xdg-desktop-portal-wlr`.

### Manual startup

At the moment, some command line flags are available for development and
testing. If you need to use one of these flags, you can start an instance of
xdpw using the following command:

```sh
xdg-desktop-portal-wlr -r [OPTION...]
```

To list the available options, you can run `xdg-desktop-portal-wlr --help`.

## FAQ

Check out or [FAQ] for answers to commonly asked questions.

Please see the [screencast compatibility] guide for more information on
compatible applications and how to get them working.

If you have a question or problem that is not mentioned in those documents,
please open an issue or come chat with us in #sway on Libera Chat.

## Contributing

If you're interested in testing or development, check out
[CONTRIBUTING.md] for more information.

## License

MIT

[xdg-desktop-portal]: https://github.com/flatpak/xdg-desktop-portal
[FAQ]: https://github.com/emersion/xdg-desktop-portal-wlr/wiki/FAQ
[screencast compatibility]: https://github.com/emersion/xdg-desktop-portal-wlr/wiki/Screencast-Compatibility
[CONTRIBUTING.md]: CONTRIBUTING.md

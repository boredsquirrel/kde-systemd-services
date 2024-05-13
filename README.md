# KDE Plasma systemd services
***Experimental*** replacement systemd services for the current xdg/autostart entries.

**Do not run this on your main system, use a VM!**

These where taken from the [Fedora Kinoite](https://fedoraproject.org/atomic-desktops/kinoite/) `/etc/xdg/autostart/` directory. This is at least one way services on Fedora KDE are started, and the goal is to find all of these ways and convert them to stable systemd user services instead.

### Why?
There are tons of issues with the current way.
- It is intransparent: many processes still run even after neutering the entries. How?
- It doesn't allow user control. `systemctl --user` works rootless and per account. It allows separate configs per user, for example having accessibility services only when needed. Many services here have no entry in systemsettings and are thus not controllable by the user.
- It is inefficient. Even though processes may be efficiently implemented, proxies and adapters (like XWaylandVideoBridge, GMenuDBusMenuProxy, XembedSniProxy) may not be needed but run anyways
- It opens attack surface without user control, like having kdeconnect-daemon run all the time, on every Plasma system. If the Firewall is not configured correctly, this could open doors

### Goal
- To find out every way Plasma services are initiated, relaunched, monitored etc. Neuter/remove them and replace them with a unified approach, being easily accessible and controllable.
- Make the services more intelligent, like only launching if the environment actually requires it.
- Keep them working as before, but allow users to opt-out of them. This should not change the current behavior, but allow changes for downstream projects or powerusers.

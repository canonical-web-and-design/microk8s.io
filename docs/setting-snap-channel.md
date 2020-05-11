---
layout: docs
title: "Selecting a snap channel"
permalink: /docs/setting-snap-channel
---

# Snap channel overview

Microk8s is a snap deploying Kubernetes. The MicroK8s snap closely follows
upstream Kubernetes, so understanding a bit about the Kubernetes release cycle
is helpful for more insight into MicroK8s releases.

Upstream Kubernetes ships a new release series (e.g. 1.17.x) approximately
every three months. Prior release series may get periodic bugfix releases: for
example, the latest 1.15 release is 1.15.5.

It is important to remember that upstream Kubernetes is committed to maintain
backwards compatibility **only within a release series**. That means that your
Kubernetes should not break when you upgrade from `v1.17.x` to `v1.17.y`, but
there is no such guarantee when upgrading from `v1.16.x` to `v1.17.x`.

## Choosing the right channel

When installing MicroK8s you can select your desired upstream Kubernetes series
by choosing the corresponding snap channel.

All the currently available channels are shown if you run `snap info microk8s`:

```
channels:
  stable:           v1.17.2         2020-01-26 (1173) 179MB classic
  candidate:        v1.17.2         2020-01-25 (1173) 179MB classic
  beta:             v1.17.2         2020-01-25 (1173) 179MB classic
  edge:             v1.17.2         2020-01-24 (1173) 179MB classic
  dqlite/stable:    –                                       
  dqlite/candidate: –                                       
  dqlite/beta:      –                                       
  dqlite/edge:      v1.16.2         2019-11-07 (1038) 189MB classic
  1.18/stable:      –                                       
  1.18/candidate:   –                                       
  1.18/beta:        –                                       
  1.18/edge:        v1.18.0-alpha.2 2020-01-22 (1172) 179MB classic
  1.17/stable:      v1.17.0         2019-12-10 (1109) 179MB classic
  1.17/candidate:   v1.17.2         2020-01-26 (1176) 179MB classic
  1.17/beta:        v1.17.2         2020-01-26 (1176) 179MB classic
  1.17/edge:        v1.17.2         2020-01-25 (1176) 179MB classic
  1.16/stable:      v1.16.4         2020-01-13 (1117) 188MB classic
  1.16/candidate:   v1.16.6         2020-01-24 (1163) 179MB classic
  1.16/beta:        v1.16.6         2020-01-24 (1163) 179MB classic
  1.16/edge:        v1.16.6         2020-01-25 (1175) 179MB classic
  1.15/stable:      v1.15.7         2020-01-06 (1114) 171MB classic
  1.15/candidate:   v1.15.9         2020-01-23 (1165) 171MB classic
  1.15/beta:        v1.15.9         2020-01-23 (1165) 171MB classic
  1.15/edge:        v1.15.9         2020-01-25 (1178) 171MB classic
  1.14/stable:      v1.14.10        2020-01-06 (1120) 217MB classic
  1.14/candidate:   v1.14.10        2019-12-14 (1120) 217MB classic
  1.14/beta:        v1.14.10        2019-12-14 (1120) 217MB classic
  1.14/edge:        v1.14.10        2020-01-26 (1181) 217MB classic
  1.13/stable:      v1.13.6         2019-06-06  (581) 237MB classic
  1.13/candidate:   v1.13.6         2019-05-09  (581) 237MB classic
  1.13/beta:        v1.13.6         2019-05-09  (581) 237MB classic
  1.13/edge:        v1.13.7         2019-06-06  (625) 244MB classic
  1.12/stable:      v1.12.9         2019-06-06  (612) 259MB classic
  1.12/candidate:   v1.12.9         2019-06-04  (612) 259MB classic
  1.12/beta:        v1.12.9         2019-06-04  (612) 259MB classic
  1.12/edge:        v1.12.9         2019-05-28  (612) 259MB classic
  1.11/stable:      v1.11.10        2019-05-10  (557) 258MB classic
  1.11/candidate:   v1.11.10        2019-05-02  (557) 258MB classic
  1.11/beta:        v1.11.10        2019-05-02  (557) 258MB classic
  1.11/edge:        v1.11.10        2019-05-01  (557) 258MB classic
  1.10/stable:      v1.10.13        2019-04-22  (546) 222MB classic
  1.10/candidate:   v1.10.13        2019-04-22  (546) 222MB classic
  1.10/beta:        v1.10.13        2019-04-22  (546) 222MB classic
  1.10/edge:        v1.10.13        2019-04-22  (546) 222MB classic
installed:          v1.17.2                    (1173) 179MB classic

```

To install the latest stable version, simply run:

```bash
snap install microk8s --classic
```

In this case you will get periodic snap updates to the latest stable release.
Bear in mind that this could include a new Kubernetes series, and therefore is
not guaranteed to continue running. For anything more than an ephemeral
Kubernetes install, you are strongly advised to select a series.

For example, to install MicroK8s and let it follow the `v1.17` stable release
series you can run:

```
snap install microk8s --classic --channel=1.17/stable
```

In this case you will only receive updates for the 1.17 release of Kubernetes,
and MicroK8s will never upgrade to 1.18, unless you explicitly
[refresh the snap](#refresh)


## Stable, candidate, beta and edge releases

The `*/stable` channels serve the latest stable upstream Kubernetes release of
the respective release series. Upstream releases are propagated to the MicroK8s
snap in about a week. This means your MicroK8s will upgrade to the latest
upstream release in your selected channel roughly one week after the upstream
release.

The `*/candidate` and `*/beta` channels get updated within hours of an upstream
release. Getting a MicroK8s deployment pointing to `1.17/beta` is as simple as:

```
snap install microk8s --classic --channel=1.17/beta
```

The `*/edge` channels get updated on each MicroK8s patch or upstream
Kubernetes patch release.

Keep in mind that edge and beta are snap constructs and do not relate to
specific Kubernetes release names.


## Tracks with pre-stable releases

On tracks where no stable Kubernetes release is available, MicroK8s ships
pre-release versions under the following scheme:

-   The `*/edge` channel (eg `1.17/edge`) holds the alpha upstream releases. 
-   The `*/beta` channel (eg `1.17/beta`) holds the beta upstream releases.
-   The `*/candidate` channel (eg `1.17/candidate`) holds the release candidate
    of upstream releases.

Pre-release versions will be available the same day they are released upstream. 

For example, to test your work against the alpha `v1.18` release simply run:

```
sudo snap install microk8s --classic --channel=1.18/edge
```

However, be aware that pre-release versions may require you to configure the
Kubernetes services on your own.


## I am confused. Which channel is right for me?

The single question you need to focus on is what channel should be used below:

```
sudo snap install microk8s --classic --channel=<which_channel?>
```

Here are some suggestions for the channel to use based on your needs:

-   I want to always be on the latest stable Kubernetes.

     -- Use `--channel=latest`

-   I want to always be on the latest release in a specific upstream K8s release.

     -- Use `--channel=<release>/stable`, eg `--channel=1.14/stable`. 

-   I want to test-drive a pre-stable release.

     -- Use `--channel=<next_release>/edge` for alpha releases.

     -- Use `--channel=<next_release>/beta` for beta releases.

     -- Use `--channel=<next_release>/candidate` for candidate releases.

-   I am waiting for a bug fix on MicroK8s:

     -- Use `--channel=<release>/edge`.

-   I am waiting for a bug fix on upstream Kubernetes:

     -- Use `--channel=<release>/candidate`.

<a id="refresh"> </a>
## Changing channels

It is possible to change the snap channel using the refresh command. E.g. to
transition from 1.17 stable to the latest alpha:

```bash
sudo snap refresh microk8s --channel=1.17/edge
```
<div class="p-notification--caution">
  <p markdown="1" class="p-notification__response">
    <span class="p-notification__status">Caution:</span>
    Changing the channel to a
    different series will almost certainly cause problems, as the configuration
    from the current version will be retained. If at all possible, it is
    recommended to re-install MicroK8s rather than refresh to a different channel,
    as it is not guaranteed to work.
  </p></div>

## Changing the refresh schedule

By default, snaps are set to check for updates and automatically refresh to the
latest version (for your selected channel) four times per day. There are some
scenarios however where it may be inconvenient or difficult to refresh the
current snap so often.

There are some controls available to set the ***global*** refresh schedule for
all snaps on the system. These are outlined in the
[Snap documentation][snap-docs].



<!-- LINKS -->
[snap-docs]:  https://snapcraft.io/docs/keeping-snaps-up-to-date#heading--controlling-updates
<!-- FEEDBACK -->
<div class="p-notification--information">
  <p class="p-notification__response">
    We appreciate your feedback on the docs. You can
    <a href="https://github.com/canonical-web-and-design/microk8s.io/edit/master/docs/setting-snap-channel.md" class="p-notification__action">edit this page</a>
    or
    <a href="https://github.com/canonical-web-and-design/microk8s.io/issues/new" class="p-notification__action">file a bug here</a>.
  </p>
</div>

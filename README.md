
# MarschallOS

A couple of images for me to learn how immutable distros work and how to build them.

Currently there are four images.

| Name | Info | Stability |
| ------ | ---------- | ---------- |
| marschallos-gnome | Fedora Silverblue + Gnome Extensions + Default & Advanced Flatpaks | Stable
| marschallos-kde | Fedora Kinoite + Default & Advanced Flatpaks | Stable
| marschallos-budgie | Fedora Budgie Atomic + Default & Advanced Flatpaks | Stable
| marschallos-sway | Fedora Sway Atomic + custom sway config, wofi, waybar + Default Flatpaks  | not stable, lots of bugs

## Applications

Following flatpaks are included:

### Default Flatpaks

  - com.bitwarden.desktop
  - org.signal.Signal
  - org.videolan.VLC
  - md.obsidian.Obsidian
  - org.localsend.localsend_app

### Advanced Flatpaks

  - com.valvesoftware.Steam
  - com.discordapp.Discord
  - com.visualstudio.code
  - com.ranfdev.DistroShelf
  - com.todoist.Todoist
  - io.podman_desktop.PodmanDesktop







This image is built with [BlueBuild](https://blue-build.org/]. 

### Installation

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/blue-build/template:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/blue-build/template:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

### ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/how-to/generate-iso/#_top). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

### Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/blue-build/template
```

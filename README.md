
# MarschallOS

An image with all the tools I need and want in an OS. 
Its based on Fedora Silverblue and Kinoite, first one for Gnome, last one for the KDE image. 

## GNOME Image
Following software ships with the GNOME image of MarschallOS:
  - com.rafaelmardojai.Blanket
  - org.gnome.Podcasts
  - dev.geopjr.Tuba
  - org.gnome.Solanum
  - org.gnome.Snapshot
  - org.gnome.Loupe
  - com.mattjakeman.ExtensionManager

### GNOME Extensions:
  - Blur my Shell
  - Dash to Dock
  - Copyous

## KDE Image

Currently only ships the flatpaks listed below. 

# Flatpaks in all images

Following flatpaks are included in both images:
  - com.valvesoftware.Steam
  - md.obsidian.Obsidian
  - com.bitwarden.desktop
  - org.signal.Signal
  - com.visualstudio.code
  - com.ranfdev.DistroShelf
  - com.todoist.Todoist
  - io.podman_desktop.PodmanDesktop
  - com.discordapp.Discord
  - org.videolan.VLC
  - org.localsend.localsend_app
    
This image is built with [BlueBuild](https://blue-build.org/). 

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

# pegasus-dx &nbsp; [![bluebuild build badge](https://github.com/pegasusandme/pegasus-dx/actions/workflows/build.yml/badge.svg)](https://github.com/pegasusandme/pegasus-dx/actions/workflows/build.yml)

See the [BlueBuild docs](https://blue-build.org/how-to/setup/) for quick setup instructions for setting up your own repository based on this template: https://github.com/blue-build/template

This is a custom image based on the Universal Blue modified Kinoite (main) image: ghcr.io/ublue-os/kinoite-main. This is pulling from "latest" and not a specific version... for now at least. 

I have added a few additional packages on top of the already-modifed base to minimize juggling of layers when deploying to my machines. You might find this useful if you like Plasma and what UBlue has added to images such as Bazzite or Aurora, but are looking for a more "vanilla" experience. This is NOT a gaming focussed spin, but can easily be tailored for that.  

My primary usage is multimedia operations and development, so I've got multimedia tools such as Handbrake, K3b, Audex, etc as well as distrobox, distroshelf, and virt-manager included here. I'm still fine tuning things as of 2/15/2026, so there will likely be daily'ish changes to the recipe.yml file until the dust settles. 

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest pegasus-dx build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/pegasusandme/pegasus-dx:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/pegasusandme/pegasus-dx:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/pegasusandme/pegasus-dx
```

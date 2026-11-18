# ingress-nginx-image

Builds the ingress-nginx controller image that Virtual Fly Brain runs on its Kubernetes cluster, from the
Chainguard-maintained fork [chainguard-forks/ingress-nginx](https://github.com/chainguard-forks/ingress-nginx).

The upstream project (kubernetes/ingress-nginx) was retired in March 2026 and its final release bundles nginx 1.27.1,
which no longer receives fixes. The Chainguard fork backports security fixes onto that nginx but publishes source
only, so this repository builds the image itself:

1. build the fork's nginx base image (`images/nginx/rootfs`), which applies the backported patches;
2. build the controller image on top of that base;
3. smoke-test it, then push `virtualflybrain/ingress-nginx-controller:<version>` to Docker Hub.

The fork version to build is in `FORK_TAG`. Change it in a pull request; the build runs on the PR as a check, and a
maintainer pushes the image by running the workflow by hand with `push` ticked.

This is a stop-gap while VFB moves to a maintained ingress controller.

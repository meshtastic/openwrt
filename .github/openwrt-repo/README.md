# Meshtastic OpenWrt Repo

Home to our APK and OPKG repositories for easily installing Meshtastic on OpenWrt-supported routers.

If you're looking for the package source code, check out [meshtastic/openwrt](https://github.com/meshtastic/openwrt).

## Supported OpenWRT versions
- `SNAPSHOT` (master branch)
- `25.12` (stable)
- `24.10` (old-stable)
- `23.05` (old-stable)
- `22.03` (old-stable)

## How to use

This repository is hosted on [Cloudflare R2](https://developers.cloudflare.com/r2/). Repositories use HTTPS protocol and require one of the SSL support packages to be installed on your router.

### APK
Used in the latest stable OpenWrt versions.

Supported versions:
- `25.12`

##### Add APK repository to your OpenWrt device

```sh
WRT_VER=$( . /etc/openwrt_release; echo "${DISTRIB_RELEASE%%-*}" | cut -d. -f1-2 )
echo "https://openwrt.meshtastic.org/openwrt-${WRT_VER}/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://openwrt.meshtastic.org/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```

---

### OPKG
Used in old-stable versions of OpenWrt.

Supported versions:
- `24.10`
- `23.05`
- `22.03`

##### Add OPKG repository to your OpenWrt device

```sh
opkg update
opkg install wget-ssl
wget -O /tmp/meshtastic-ipk.pub https://openwrt.meshtastic.org/meshtastic-ipk.pub
opkg-key add /tmp/meshtastic-ipk.pub && rm /tmp/meshtastic-ipk.pub
sed -i '/meshtastic/d' /etc/opkg/customfeeds.conf
ARCH=$( . /etc/openwrt_release; echo "$DISTRIB_ARCH" )
WRT_VER=$( . /etc/openwrt_release; echo "${DISTRIB_RELEASE%%-*}" | cut -d. -f1-2 )
echo "src/gz meshtastic https://openwrt.meshtastic.org/openwrt-${WRT_VER}/${ARCH}" >> /etc/opkg/customfeeds.conf
opkg update
```

---

### Snapshot (master) builds

For testing only. Please do not file issues about SNAPSHOT builds.

##### Add APK repository to your OpenWrt device

```sh
echo "https://openwrt.meshtastic.org/main/$(cat /etc/apk/arch)/packages.adb" > /etc/apk/repositories.d/meshtastic.list
wget https://openwrt.meshtastic.org/meshtastic-apk.pem -O /etc/apk/keys/meshtastic-apk.pem
apk update
```
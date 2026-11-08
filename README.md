# Termux:Boot (e16tae fork)

Termux:Boot built and signed with the e16tae key, for use with the [e16tae Termux app](https://github.com/e16tae/termux-app). It is not an official Termux release and is not affiliated with the Termux project.

- **Install:** download the APK from [Releases](https://github.com/e16tae/termux-boot/releases/latest). It only works with the e16tae Termux app, because Termux plugins must share the app's signing key.
- **Signing certificate SHA-256:** `BF:E9:7B:F9:77:33:40:76:8E:BE:B7:B2:CA:8C:FD:83:40:5E:96:50:0B:39:1B:43:E0:54:2B:F5:AA:F0:44:EF`
- **Changes:** see [CHANGELOG.md](CHANGELOG.md). Branches: `main` (released), `dev` (work in progress).

<details>
<summary>한국어</summary>

[e16tae Termux 앱](https://github.com/e16tae/termux-app)과 함께 쓰도록 e16tae 키로 빌드하고 서명한 Termux:Boot입니다. Termux 공식 릴리스가 아니며 Termux 프로젝트와 관계가 없습니다.

- **설치:** [Releases](https://github.com/e16tae/termux-boot/releases/latest)에서 APK를 받습니다. Termux 플러그인은 앱과 같은 서명 키를 써야 하므로 e16tae Termux 앱에서만 동작합니다.
- **서명 인증서 SHA-256:** 위와 같습니다.
- **변경 사항:** [CHANGELOG.md](CHANGELOG.md)를 보세요. 브랜치: `main`(배포), `dev`(작업 중).

</details>

---

# Termux:Boot

[![Build status](https://github.com/termux/termux-boot/workflows/Build/badge.svg)](https://github.com/termux/termux-boot/actions)
[![Join the chat at https://gitter.im/termux/termux](https://badges.gitter.im/termux/termux.svg)](https://gitter.im/termux/termux)

A [Termux](https://termux.dev) add-on app to run programs at boot.

When developing (or packaging), note that this app needs to be signed with the
same key as the main Termux app in order to have the permission to execute scripts.

## Installation

Termux:Boot application can be obtained from [F-Droid](https://f-droid.org/en/packages/com.termux.boot/).

Additionally we provide per-commit debug builds for those who want to try
out the latest features or test their pull request. This build can be obtained
from one of the workflow runs listed on [Github Actions](https://github.com/termux/termux-boot/actions/workflows/github_action_build.yml?query=branch%3Amaster+event%3Apush)
page.

Signature keys of all offered builds are different. Before you switch the
installation source, you will have to uninstall the Termux application and
all currently installed plugins. Check https://github.com/termux/termux-app#Installation for more info.

## How to use

1. Install the Termux:Boot app.
2. Start the Termux:Boot app once by clicking on its launcher icon. This allows the app to be run at boot.
3. Create the `~/.termux/boot/` directory.
4. Put scripts you want to execute inside the `~/.termux/boot/` directory. If there are multiple files, they will be executed in a sorted order.
5. Note that you may want to run `termux-wake-lock` as first thing if you want to ensure that the device is prevented from sleeping.

### Examples

To start an sshd server and prevent the device from sleeping at boot,
create the following file at `~/.termux/boot/start-sshd`:

```sh
#!/data/data/com.termux/files/usr/bin/sh
termux-wake-lock
sshd
```

To start
[termux-services](https://wiki.termux.com/wiki/Termux-services), which
in turn starts enabled services, you can put the following in
`~/.termux/boot/start-services`:

```sh
#!/data/data/com.termux/files/usr/bin/sh
termux-wake-lock
source /data/data/com.termux/files/usr/etc/profile.d/start-services.sh
```

## License

Released under [the GPLv3 license](https://www.gnu.org/licenses/gpl.html).

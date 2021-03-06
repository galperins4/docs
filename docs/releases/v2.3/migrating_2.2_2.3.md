# Migrating from v2.2 to v2.3

Upgrading from `v2.2` to `v2.3` is fairly straightforward if you follow the instructions. Even though we try to ensure backward compatibility (BC) as much as possible, sometimes it is not possible or very complicated to avoid it and still create a good solution to a problem.

::: warning
Upgrading a complex software project always comes at the risk of breaking something, so make sure you have a backup.
:::

### Notes

After upgrading you should check whether your application still works as expected and no plugins are broken. See the following notes on which changes to consider when upgrading from one version to another.

## Prerequisites

::: warning
Be sure to complete all of the following changes before you continue to upgrade to the latest version.
:::

### Configuration

- Since 2.3 we no longer ship `@arkecosystem/core-logger-winston` by default, open the `~/.config/ark-core/<network>/plugins.js` file (e.g. for mainnet using nano you would run `nano ~/.config/ark-core/mainnet/plugins.js`), locate the `@arkecosystem/core-logger-winston` plugin and replace it like shown below.

#### Old

```js
"@arkecosystem/core-logger-winston": {
    transports: {
        console: {
            options: {
                level: process.env.CORE_LOG_LEVEL || "debug",
            },
        },
        dailyRotate: {
            options: {
                level: process.env.CORE_LOG_LEVEL || "debug",
            },
        },
    },
},
```

#### New

```js
"@arkecosystem/core-logger-pino": {},
```

> If you are using the plugin and want to continue using it you need to run `yarn global add @arkecosystem/core-logger-winston` and leave your configuration unchanged.

### [DEVNET ONLY] Switching to the `next` release channel

During the development of 2.2.0 there were the channels `alpha`, `beta` and `rc` as a lot of testing had to be done before going public with the switch from using a git repository to providing a CLI. Run the following command to install the 2.3.0 release.

```shell
yarn global add @arkecosystem/core@next
```

From 2.3.0 onwards the `next` channel will serve as a combination of all of the old channels on `devnet`. This means there won't be the need to switch between alpha, beta or rc anymore.

## Upgrade Steps

::: warning
Do not run any of the mentioned commands with `sudo` unless explicitly stated.
:::

### Installing 2.3.0

```bash
ark update
```

## Reporting Problems

If you happen to experience any issues please [open an issue](https://github.com/ArkEcosystem/core/issues/new?template=Bug_report.md) with a detailed description of the problem, steps to reproduce it and info about your environment.

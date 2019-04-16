# Customize Plus Builder [![by KnitKode](https://img.shields.io/badge/by-KnitKode-lightgrey.svg?style=social)](https://knitkode.com)

[![GitHub release](https://img.shields.io/github/release/knitkode/customize-plus-builder.svg)](https://github.com/knitkode/customize-plus-builder/releases/latest)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

> Building Theme options for the WordPress Customizer has never been easier.

## Free vs Premium

Customize Plus Builder comes in **two versions**:

* ‎a *free* [standalone static web application](https://knitkode.com/customize-plus-builder)
* ‎a *premium* [WordPress plugin](https://knitkode.com/products/customize-plus-builder)

The two versions have the same functionalities in regards to building a [customizer tree](https://knitkode.com/customize-plus-builder#customizer-tree) and are always updated at the same time. Their difference is that only with the WordPress plugin you can save, edit and manage your [customizer trees](https://knitkode.com/customize-plus-builder#tree-manager) in the WordPress installation of your choice. This gives you the freedom and comfortableness of build and tweak, update and release your customizer trees step by step.

## Bugs

If you find an issue, please let us know [here](https://github.com/knitkode/customize-plus-builder/issues?state=open), thanks!

## Support

This is a developer's portal and should **not** be used for support but only for development. Please visit the [support page](https://knitkode.com/support) to see other options.

You can also try to see if someone is in our [chat room](https://gitter.im/knitkode/customize-plus-builder):

[![Gitter Chat](http://img.shields.io/badge/GITTER-JOIN%20CHAT-1DCE73.svg)](https://gitter.im/knitkode/customize-plus-builder)

## Contribute

Anyone is welcome to contribute, there are various ways you can do it:

1. Raise an [issue](https://github.com/knitkode/customize-plus-builder/issues) on GitHub
2. Provide feedback and suggestions on [enhancements](https://github.com/knitkode/customize-plus-builder/issues?direction=desc&labels=Enhancement&page=1&sort=created&state=open)

## Donate

[![Liberapay](https://img.shields.io/liberapay/KnitKode/receives.svg)](https://liberapay.com/KnitKode/donate)

## Development

### `customize-plus` as a local dependency

To include `customize-plus` in dev environment you can link the local repo. To do so: `cd` to `customize-plus` root project folder and run `yarn-link`, then `cd` in this project root folder and run `yarn link @knitkode/customize-plus`, then you might need to change these two npm scripts in the root `package.json`:

```js
"prewatch": "yarn link @knitkode/customize-plus",
"init": "git submodule add git@gitlab.com:kuus/dev-lib config/dev-lib && cd packages/app && yarn link @knitkode/customize-plus",
```

You might want to do the same for the package `@knitkode/dashicons`.

### Components hierarchy

* Each CustomizerComponent class defines its schema of args.
* Each CustomizerComponent has its own `Editor${ComponentType}.js` whic

```js
Editor
|_EditorPanel // redux update model happens here
| |_...EditorPanelArg (main)
|   |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
| |_EditorArgsGroup (advanced)
|  |_...EditorPanelArg
|     |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
|_EditorSection // redux update model happens here
| |_...EditorSectionArg (main)
|   |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
| |_EditorArgsGroup (advanced)
|  |_..._EditorSectionArg
|     |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
|_EditorField // redux update model happens here
  |_EditorControl
  | |_EditorArgsGroup (main)
  | | |_...EditorFieldArg || ControlSpecifcArg
  | |   |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
  | |_EditorArgsGroup (basic)
  | | |_...EditorFieldArg
  | |   |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
  | |_EditorArgsGroup (specific)
  |   |_...EditorFieldArg
  |     |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
  |_EditorSetting
  | |_SettingDefaultArg || EditorFieldArg (default)
  | | |_Arg
  | |_EditorArgsGroup (basic)
  | | |_...EditorFieldArg
  | |   |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
  | |_EditorArgsGroup (advanced)
  |   |_...EditorFieldArg
  |     |_...EditorArg (ArgString | ArgArray | ArgColor | etc.)
```

### Validation

Validation is used to validate a tree client side. The goal is to make it almost impossible for the user to save or export an invalid Customizer Tree. It is performed in **two times**:

1. on change of any model value of the currently editing Customizer Component (`panel/section/field(control/setting)`);
2. on saving and on export, applying to all the Customizer Tree, preventing those actions to succeed in case of validation failure.

The validation process occours at **two levels**:

1. at the **schema definition**, each `arg` can specify an array of validator functions (e.v. `isId`, `isFloat`, ecc.) and of validator error messages respectively in the properties `$builderValidators` and `$builderErrors` of each `arg`
2. at the **customize component model** level, that is in each Customizer Component model class (e.g. `controls/color/index.js`), here are managed validation logics that take in account the relationship between various `args` set on the model instance. Each model class can override the method `$builderValidate` where to

### TODO

* [x] Tree validation client side
* [ ] Tree validation server side

## License

 [![License](https://img.shields.io/badge/license-MIT-blue.svg)](http://doge.mit-license.org) [![KnitKode](https://img.shields.io/badge/%C2%A9KnitKode-2017-blue.svg)](https://knitkode.com)

- - - -

:registered: KnitKode 2018 | [knitkode.com](https://knitkode.com) | dev@knitkode.com

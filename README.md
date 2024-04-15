# Nextcloud Prettier configuration

This provides a shared configuration for Nextcloud apps and libraries to have consistent stylistic rules.
Using stylistic rules in linters is not recommended as linters are for finding bugs while prettier is for code style.
Moreover ESLint and StyleLint both deprecate and remove stylistic rules, as a replacement using Prettier is recommended.

## Setup
### Prepare ESLint
If you are using ESLint you should enable the `eslint-config-prettier` configuration which disables all ESLint rules that conflict with Prettier.
A detailed description can be found here: [github.com/prettier/eslint-config-prettier](https://github.com/prettier/eslint-config-prettier?tab=readme-ov-file#installation).

In short, this should be your ESLint config:
```json
{
  "extends": [
    "@nextcloud",
    "prettier" // < this needs to be the last one to override all previous
  ]
}
```

If you still get errors about Vue files, you need to adjust your ESLint config like the following:
*(this will be fixed once the Nextcloud ESLint config support flat configs)*

```json
"extends": [
		"@nextcloud",
		"prettier"
	],
	"overrides": [
		{
			"files": ["**/*.vue"],
			"rules": {
				"vue/first-attribute-linebreak": "off"
			}
		}
	]
```

### Prepare StyleLint
Stylelint already removed all stylistic rules, so make sure to use `@nextcloud/stylelint-config` **3+** together with `stylelint` 16+.

### Configure Prettier
Install this configuration using:
```shell
npm install --save-dev @nextcloud/prettier-config
```

Either configure Prettier within your `package.json`:
```json
{
  "name": "nextcloud-app",
  "version": "1.33.7",
  "prettier": "@nextcloud/prettier-config"
}
```

Or in a dedicated `.prettierrc.json`:
```json
"@nextcloud/prettier-config"
```

<!--
  SPDX-FileCopyrightText: 2024 Nextcloud contributors
  SPDX-License-Identifier: CC0-1.0
-->

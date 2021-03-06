# d2l-labs-accordion

[![NPM version](https://img.shields.io/npm/v/@brightspace-ui-labs/accordion.svg)](https://www.npmjs.org/package/@brightspace-ui-labs/accordion)

> Note: this is a ["labs" component](https://github.com/BrightspaceUI/guide/wiki/Component-Tiers). While functional, these tasks are prerequisites to promotion to BrightspaceUI "official" status:
>
> - [ ] [Design organization buy-in](https://github.com/BrightspaceUI/guide/wiki/Before-you-build#working-with-design)
> - [ ] [design.d2l entry](http://design.d2l/)
> - [ ] [Architectural sign-off](https://github.com/BrightspaceUI/guide/wiki/Before-you-build#web-component-architecture)
> - [x] [Continuous integration](https://github.com/BrightspaceUI/guide/wiki/Testing#testing-continuously-with-travis-ci)
> - [x] [Cross-browser testing](https://github.com/BrightspaceUI/guide/wiki/Testing#cross-browser-testing-with-sauce-labs)
> - [ ] [Unit tests](https://github.com/BrightspaceUI/guide/wiki/Testing#testing-with-polymer-test) (if applicable)
> - [ ] [Accessibility tests](https://github.com/BrightspaceUI/guide/wiki/Testing#automated-accessibility-testing-with-axe)
> - [ ] [Visual diff tests](https://github.com/BrightspaceUI/visual-diff)
> - [x] [Localization](https://github.com/BrightspaceUI/guide/wiki/Localization) with Serge (if applicable)
> - [x] Demo page
> - [ ] README documentation

Polymer-based widget that displays a list of collapsible components. When collapsible component is clicked - it expands or collapses the associated content.

## Installation

```shell
npm install @brightspace-ui-labs/accordion
```

## Polymer components:
### **d2l-labs-accordion** - accordion panel.
#### Attributes:
* multi - allows multiple collapsibles to be opened at the same time
* selected - used only if `multi` is disabled. sets item index to be opened by default
* selectedValue - used only if `multi` is set. Sets array of indexes for the items to be opened by default
* autoClose - expanding any **d2l-labs-accordion-collapse** child (except those that are disabled) will automatically close other opened children.
### **d2l-labs-accordion-collapse** - accordion component.
#### Attributes:
* flex - adjust component to the parent width
* noIcons - hide the expand/collapse icon
* opened - container is opened by default. Do not use this attribute when inside the **d2l-labs-accordion** as the **d2l-labs-accordion** does not monitor opened state of the items at the start. In this case, use `selected` or `selectedValue` **d2l-labs-accordion** attributes instead.
* disabled - container cannot be expanded or collapsed
* disable-default-trigger-focus - disables the default outline added by browsers on trigger focus so custom styles can be added to the component on focus
* headerBorder - show a border between the header and the summary/content
* icon-has-padding - adds padding on one side of the icon.
  * When used with 'flex' attribute, the padding will be to the right. (Opposite for RTL)
  * Without 'flex' attribute, the padding will be on the left. (Opposite for RTL)

#### Slots:
* header - content to display under the title
* summary - content that summarizes the data inside the accordion

Example 1:
```html
<d2l-labs-accordion selected="1">
	<d2l-labs-accordion-collapse title="Item 1" flex>
		Text 1
	</d2l-labs-accordion-collapse>
	<d2l-labs-accordion-collapse title="Item 2" flex>
		Item 3
	</d2l-labs-accordion-collapse>
	<d2l-labs-accordion-collapse title="Item 3" flex>
		Text 3
	</d2l-labs-accordion-collapse>
</d2l-labs-accordion>
```

Example 2:
```html
<d2l-labs-accordion multi selectedValue="[1,2]">
	<d2l-labs-accordion-collapse title="Item 1" flex>
		Text 1
	</d2l-labs-accordion-collapse>
	<d2l-labs-accordion-collapse title="Item 2" flex>
		Item 3
	</d2l-labs-accordion-collapse>
	<d2l-labs-accordion-collapse title="Item 3" flex>
		Text 3
	</d2l-labs-accordion-collapse>
</d2l-labs-accordion>
```

Example 3:
```html
<d2l-labs-accordion-collapse title="Opened By Default (Flex)" opened flex>
	Text 1
</d2l-labs-accordion-collapse>
```

Example 4:
```html
<d2l-labs-accordion-collapse title="Opened By Default (Regular)" opened>
	Text 1
</d2l-labs-accordion-collapse>
```

Example 5:
```html
<d2l-labs-accordion-collapse flex header-border>
	<h2 slot="header">Custom header, summary, border and flex 💪</h2>
	<ul slot="summary" style="list-style-type: none; padding-left: 0px;">
		<li>Availability starts 4/13/2020 and ends 4/23/2020</li>
		<li>One release condition</li>
		<li>Special access</li>
	</ul>
	<p>Stuff inside of the accordion goes here</p>
</d2l-labs-accordion-collapse>
```
## Developing, Testing and Contributing

After cloning the repo, install dependencies:
```shell
npm install
```

If you don't have it already, install the [Polymer CLI](https://www.polymer-project.org/2.0/docs/tools/polymer-cli) globally:

```shell
npm install -g polymer-cli
```

To start a [local web server](https://www.polymer-project.org/2.0/docs/tools/polymer-cli-commands#serve) that hosts the demo page and tests:

```shell
npm start
```

To access the demo page visit [http://127.0.0.1:8081/components/d2l-labs-accordion/demo/](http://127.0.0.1:8081/components/d2l-labs-accordion/demo/)

To lint ([eslint](http://eslint.org/) and [Polymer lint](https://www.polymer-project.org/2.0/docs/tools/polymer-cli-commands#lint)):

```shell
npm run lint
```

To run unit tests locally using [Polymer test](https://www.polymer-project.org/2.0/docs/tools/polymer-cli-commands#tests):

```shell
npm run test:polymer:local
```

To lint AND run local unit tests:

```shell
npm test
```

## Versioning & Releasing

> TL;DR: Commits prefixed with `fix:` and `feat:` will trigger patch and minor releases when merged to `master`. Read on for more details...

The [sematic-release GitHub Action](https://github.com/BrightspaceUI/actions/tree/master/semantic-release) is called from the `release.yml` GitHub Action workflow to handle version changes and releasing.

### Version Changes

All version changes should obey [semantic versioning](https://semver.org/) rules:
1. **MAJOR** version when you make incompatible API changes,
2. **MINOR** version when you add functionality in a backwards compatible manner, and
3. **PATCH** version when you make backwards compatible bug fixes.

The next version number will be determined from the commit messages since the previous release. Our semantic-release configuration uses the [Angular convention](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-angular) when analyzing commits:
* Commits which are prefixed with `fix:` or `perf:` will trigger a `patch` release. Example: `fix: validate input before using`
* Commits which are prefixed with `feat:` will trigger a `minor` release. Example: `feat: add toggle() method`
* To trigger a MAJOR release, include `BREAKING CHANGE:` with a space or two newlines in the footer of the commit message
* Other suggested prefixes which will **NOT** trigger a release: `build:`, `ci:`, `docs:`, `style:`, `refactor:` and `test:`. Example: `docs: adding README for new component`

To revert a change, add the `revert:` prefix to the original commit message. This will cause the reverted change to be omitted from the release notes. Example: `revert: fix: validate input before using`.

### Releases

When a release is triggered, it will:
* Update the version in `package.json`
* Tag the commit
* Create a GitHub release (including release notes)
* Deploy a new package to NPM

### Releasing from Maintenance Branches

Occasionally you'll want to backport a feature or bug fix to an older release. `semantic-release` refers to these as [maintenance branches](https://semantic-release.gitbook.io/semantic-release/usage/workflow-configuration#maintenance-branches).

Maintenance branch names should be of the form: `+([0-9])?(.{+([0-9]),x}).x`.

Regular expressions are complicated, but this essentially means branch names should look like:
* `1.15.x` for patch releases on top of the `1.15` release (after version `1.16` exists)
* `2.x` for feature releases on top of the `2` release (after version `3` exists)

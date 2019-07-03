# Framer Bridge Starter Kit

Framer Bridge is a suite of tools:

- That allows you to automatically publish and distribute components to designers with [Framer](https://framer.com) and the [Framer Store](https://store.framer.com).
- Import in production components built by your engineers. It’s an automatic and continually synced workflow, one that is customizable to your existing development workflow.

This repository links together [folder backed Framer projects](https://www.framer.com/support/using-framer-x/folder-backed-projects/) with the [Framer CLI](https://www.npmjs.com/package/framer-cli) and [GitHub actions](https://github.com/framer/PublishAction)/[CircleCI](https://circleci.com/integrations/github/)/[Travis CI](https://travis-ci.com/) with [Greenkeeper](https://greenkeeper.io/) for an easy package publication flow.

## 🏁 Getting started

#### Cloning

1. [Fork this repository](https://help.github.com/en/articles/fork-a-repo).
1. [Clone the forked repository](https://help.github.com/en/articles/cloning-a-repository) locally
1. Run `yarn add my-design-system` to install your design system as a dependency

This repository contains one main folder, called `design-system.framerfx`, a [folder backed project](https://framer.gitbook.io/teams/integrations#folder-projects) that you can import your components from `my-design-system` and (optionally) add [interface properties](https://www.framer.com/api/property-controls/) to use in Framer. This is the project that gets published to the [Framer store](https://store.framer.com).

#### Editing

From here, you can continue modifying the existing [`design-system.framerfx`](/design-system.framerfx) file by adding your components from `my-design-system` into the [`code`](/code) folder.

An example component in the [`code`](/code) folder might look something like this:

```typescript
import * as React from "react";
import { Button as _Button } from "my-design-system";

type Props = {
  width: number;
  height: number;
};

export function Button(props: Props) {
  return <_Button {...props} />;
}

Button.defaultProps = {
  width: 150,
  height: 50
};
```

#### Publishing

1. From the terminal, run:
   ```sh
   npx framer-cli authenticate <your-framer-account-email>
   ```
1. **If the package has not been previously published to the store**, publish the package for the first time by running
   ```sh
   env FRAMER_TOKEN=<token> npx framer-cli publish <package-name.framerfx> --new="<Display Name>"
   ```

You can read more about the Framer Bridge publishing flow in the [docs](https://www.framer.com/support/using-framer-x/publishing-from-cli/). Alternatively, you can also follow the normal [publishing flow](https://www.framer.com/support/using-framer-x/publishing-packages/) to create your package in the Team Store.

## 🚚 Using CI

In order to keep the Framer X package in the Store up to date with the latest version of your NPM package, you'll want to use a few CI tools to help us manage these updates. Below is an example of a setup using [Greenkeeper](https://greenkeeper.io/) and [CircleCI](https://circleci.com/).

There is a small [CircleCI configuration](https://circleci.com/docs/2.0/configuration-reference) included in this repository that publishes the updated package to the [Framer store](https://store.framer.com) every time an update to `my-design-system` is published to NPM. You can change the [config.yml](/.circleci/config.yml) configuration to match a number of different setups, but the one included in this project will update any time the package in npm is updated.

---

**To integrate with CircleCI:**

1. [Connect your repository with CircleCI](https://circleci.com/integrations/github/).
1. Add the `FRAMER_TOKEN` environment variable in the [CI project settings](https://circleci.com/docs/2.0/env-vars/#setting-an-environment-variable-in-a-project).

---

**To integrate with Travis CI:**

1. [Connect your repository with Travis CI](https://docs.travis-ci.com/user/tutorial/#to-get-started-with-travis-ci).
1. Add the `FRAMER_TOKEN` environment variable in the [CI project settings](https://docs.travis-ci.com/user/environment-variables).

---

You'll also need to hook up your forked Github repository with a dependency manager tool like Greenkeeper, so it can can automatically update your dependencies in `design-system.framerfx`, or make a Pull Request if the version has potential breaking changes.

If a Pull Request is submitted by Greenkeeper, you may need to merge the pull request before CircleCI can publish your package to the Framer Team Store.

**To integrate with Greenkeeper:**

1. Sign up for a free [Greenkeeper Account](https://greenkeeper.io/)
1. [Connect your repository with Greenkeeper](https://greenkeeper.io/).

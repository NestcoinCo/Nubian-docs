---
description: Want to fix a bug on the application interface? Feel free.
---

# Frontend

The Nubian Finance application has its code hosted at [nubian-frontend](https://github.com/Open-Currency-Collective/nubian-frontend) it's a simple React application written using [Typescript](https://typescriptlang.org/). If you do find issues you can't resolve please don't hesitate to open an issue on the repository. We'll try our best to attend to it as soon as possible. If you do find issues you can resolve follow this guide to ensure your pull request is merged.

#### Setup your Dev Environment

1. Fork the repository, create a [draft pull request](https://github.blog/2019-02-14-introducing-draft-pull-requests/) and clone to your local machine and add the official repository as an upstream branch. The git snippet below adds nubian-frontend as an upstream branch.

```text
$ git remote add upstream https://github.com/Open-Currency-Collective/nubian-frontend.git
```

2.  Make sure you have the latest version of the default branch. The git snippet below switches to the default branch and fetches the latest code.

```text
$ git checkout master
$ git pull upstream master
```

3. Create your branch and install dependencies. The line in the snippet below creates a branch and switches to it while the next installs the dependencies.

```text
$ git checkout -b branch-name
$ yarn
```

4. Thanks for contributing your bit. Happy Coding🎉. 

{% hint style="info" %}
Create a [draft pull request](https://github.blog/2019-02-14-introducing-draft-pull-requests/) to keep the team abreast with your progress and problems you may encounter
{% endhint %}

#### Creating Pull Requests

* It is recommended for you to create a [draft pull request](https://github.blog/2019-02-14-introducing-draft-pull-requests/) to keep the team abreast with your progress and it gives you a better chance of having your pull request merged.
* Your pull request should have a **good description** of what exactly it is trying to achieve.
* Your pull request should be as small as possible. If it is going to be a major change do reach out to the team using dev@nestcoin.com.


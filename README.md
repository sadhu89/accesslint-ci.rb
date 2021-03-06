# Accesslint::Ci

Runs accesslint-cli in CircleCI and comments on GitHub pull requests with new
accessibility issues.

accesslint-ci will crawl a host site and run accessibility assertions on the
pages. If there are any new accessibility issues, accesslint-ci will comment on
the pull request that initiated the build in CircleCI.

[View an example](https://github.com/accesslint/bourbon.io/pull/1)

## Installation

1. Set up your CircleCI environment (API tokens for CircleCI and GitHub, artifacts)
1. Install dependencies (nodejs, `accesslint-cli`, `accesslint-ci`)
1. Start a development server
1. Run `accesslint-ci scan <development server e.g. http://localhost:3000>`

In your `circle.yml` file:

```
general:
  artifacts:
    - "accesslint.log"

machine:
  environment:
    CIRCLE_TOKEN: <CircleCI API token>
    ACCESSLINT_GITHUB_TOKEN: <GitHub Personal Access Token>
  node:
    version: 6.1.0

dependencies:
  override:
    - npm install -g accesslint-cli
    - gem install accesslint-ci

test:
  post:
    - bundle exec rails server
    - accesslint-ci scan http://localhost:3000
```

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).


# Patrones de examen de secretos admitidos

Listas de los secretos admitidos y los asociados con los que trabaja GitHub para evitar el uso fraudulento de secretos que se confirmaron por accidente.

## About secret scanning patterns

There are three types of secret scanning alerts:

* **User alerts:** Reported to users in the **Security** tab of the repository, when a supported secret is detected in the repository.
* **Push protection alerts:** Reported to users in the **Security** tab of the repository, when a contributor bypasses push protection.
* **Partner alerts:** Reported directly to secret providers that are part of secret scanning's partner program. These alerts are not reported in the **Security** tab of the repository.

For in-depth information about each alert type, see [About secret scanning alerts](/es/code-security/secret-scanning/managing-alerts-from-secret-scanning/about-alerts).

For details about all the supported patterns, see the [Supported secrets](#supported-secrets) section below.

If you use the REST API for secret scanning, you can use the `Secret type` to report on secrets from specific issuers. For more information, see [REST API endpoints for secret scanning](/es/rest/secret-scanning).

If you believe that secret scanning should have detected a secret committed to your repository, and it has not, you first need to check that GitHub supports your secret. For more information, refer to the following sections. For more advanced troubleshooting information, see [Secret scanning detection scope](/es/code-security/secret-scanning/troubleshooting-secret-scanning-and-push-protection/troubleshooting-secret-scanning).

## Supported secrets

The tables list the secrets supported by secret scanning for each secret type. Information in the tables may include this data:

* **Provider:** Name of the token provider.
* **Partner:** Token for which leaks are reported to the relevant token partner. Applies to public repositories and all gists, including secret gists. Secret gists are not private and can be accessed by anyone with the URL. See [About gists](/es/get-started/writing-on-github/editing-and-sharing-content-with-gists/creating-gists#about-gists).
* **User:** Token for which leaks are reported to users on GitHub.
  * Applies to public repositories, and to private repositories where GitHub Secret Protection and secret scanning are enabled.
  * Includes default tokens, which relate to supported patterns and specified custom patterns, as well as non-provider tokens such as private keys, which usually have a higher ratio of false positives.
  * For secret scanning to scan for non-provider patterns, the detection of non-provider patterns must be enabled for the repository or the organization. For more information, see [Enabling secret scanning for your repository](/es/code-security/secret-scanning/enabling-secret-scanning-features/enabling-secret-scanning-for-your-repository).
* **Push protection:** Token for which leaks are reported to users on GitHub. Applies to repositories with secret scanning and push protection enabled.
* **Validity check:** Token for which a validity check is implemented. For partner tokens, GitHub sends the token to the relevant partner. Note that not all partners are based in the United States. For more information, see [Advanced Security](/es/site-policy/github-terms/github-terms-for-additional-products-and-features#advanced-security) in the Site Policy documentation.
* **Metadata check:** Token for which extended metadata is available, providing additional context about the detected secret.
* **Base64:** Token for which Base64-encoded versions are supported.

### Non-provider patterns

Precision levels are estimated based on the pattern type's typical false positive rates.

| Provider | Token                                | Description                                                            | Precision |
| :------- | :----------------------------------- | :--------------------------------------------------------------------- | :-------- |
| Generic  | ec\_private\_key                     | Elliptic Curve (EC) private keys used for cryptographic operations     | High      |
| Generic  | generic\_private\_key                | Cryptographic private keys with `-----BEGIN PRIVATE KEY-----` header   | High      |
| Generic  | http\_basic\_authentication\_header  | HTTP Basic Authentication credentials in request headers               | Medium    |
| Generic  | http\_bearer\_authentication\_header | HTTP Bearer tokens used for API authentication                         | Medium    |
| Generic  | mongodb\_connection\_string          | Connection strings for MongoDB databases containing credentials        | High      |
| Generic  | mysql\_connection\_string            | Connection strings for MySQL databases containing credentials          | High      |
| Generic  | openssh\_private\_key                | OpenSSH format private keys used for SSH authentication                | High      |
| Generic  | pgp\_private\_key                    | PGP (Pretty Good Privacy) private keys used for encryption and signing | High      |
| Generic  | postgres\_connection\_string         | Connection strings for PostgreSQL databases containing credentials     | High      |
| Generic  | rsa\_private\_key                    | RSA private keys used for cryptographic operations                     | High      |

> \[!NOTE]
> Validity checks are **not supported** for non-provider patterns.

### Copilot secret scanning

Secret scanning uses Copilot to detect generic passwords. See [Responsible detection of generic secrets with Copilot secret scanning](/es/code-security/secret-scanning/copilot-secret-scanning/responsible-ai-generic-secrets).

| Provider | Token    |
| -------- | :------- |
| Generic  | password |

> \[!NOTE] Push protection and validity checks are not supported for passwords.

### Default patterns

> \[!NOTE]
> Validity and extended metadata checks are only available to users with GitHub Team or GitHub Enterprise who enable the feature as part of GitHub Secret Protection.

| Provider                       | Token                                                                                                           |                                  Partner                                  |                                    User                                   |                              Push protection                              |                               Validity check                              |                               Metadata check                              |                                   Base64                                  |
| ------------------------------ | :-------------------------------------------------------------------------------------------------------------- | :-----------------------------------------------------------------------: | :-----------------------------------------------------------------------: | :-----------------------------------------------------------------------: | :-----------------------------------------------------------------------: | :-----------------------------------------------------------------------: | :-----------------------------------------------------------------------: |
| 1Password                      | 1password\_service\_account\_token                                                                              |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Adafruit                       | adafruit\_io\_key                                                                                               | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Adobe                          | adobe\_client\_secret                                                                                           | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Adobe                          | adobe\_device\_token                                                                                            | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Adobe                          | adobe\_pac\_token                                                                                               | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Adobe                          | adobe\_refresh\_token                                                                                           | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Adobe                          | adobe\_service\_token                                                                                           | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Adobe                          | adobe\_short\_lived\_access\_token                                                                              | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Aikido                         | aikido\_api\_client\_secret                                                                                     |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Aikido                         | aikido\_ci\_scanning\_token                                                                                     |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Airtable                       | airtable\_api\_key                                                                                              |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Airtable                       | airtable\_personal\_access\_token                                                                               |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Aiven                          | aiven\_auth\_token                                                                                              | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Aiven                          | aiven\_service\_password                                                                                        | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Alibaba                        | alibaba\_cloud\_access\_key\_id, </br>alibaba\_cloud\_access\_key\_secret                                       | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Amazon AWS                     | aws\_access\_key\_id, </br>aws\_secret\_access\_key <br/><a href="#token-versions">Token versions</a>           | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |
| Amazon AWS                     | aws\_api\_key                                                                                                   | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Amazon AWS                     | aws\_secret\_access\_key, </br>aws\_session\_token, </br>aws\_temporary\_access\_key\_id                        |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Anthropic                      | anthropic\_admin\_api\_key                                                                                      | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |
| Anthropic                      | anthropic\_api\_key <br/><a href="#token-versions">Token versions</a>                                           | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |
| Anthropic                      | anthropic\_session\_id                                                                                          | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> | <span role="img" class="octicon-bg-check" aria-label="Supported">✓</span> |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-label="Unsupported">✗</span>  |  <span role="img" class="octicon-bg-x" aria-

# Contributor Covenant Code of Conduct
Edgar Manuel Ruiz Arias 
## Our Pledge

We as members, contributors, and leaders pledge to make participation in our
community a harassment-free experience for everyone, regardless of age, body
size, visible or invisible disability, ethnicity, sex characteristics, gender
identity and expression, level of experience, education, socio-economic status,
nationality, personal appearance, race, religion, or sexual identity
and orientation.

We pledge to act and interact in ways that contribute to an open, welcoming,
diverse, inclusive, and healthy community.

## Our Standards

Examples of behavior that contributes to a positive environment for our
community include:

* Demonstrating empathy and kindness toward other people
* Being respectful of differing opinions, viewpoints, and experiences
* Giving and gracefully accepting constructive feedback
* Accepting responsibility and apologizing to those affected by our mistakes,
  and learning from the experience
* Focusing on what is best not just for us as individuals, but for the
  overall community

Examples of unacceptable behavior include:

* The use of sexualized language or imagery, and sexual attention or
  advances of any kind
* Trolling, insulting or derogatory comments, and personal or political attacks
* Public or private harassment
* Publishing others' private information, such as a physical or email
  address, without their explicit permission
* Unsolicited or unwanted messaging, including outreach via personal contact
  information, social media platforms, or other communication channels to draw
  attention to contributions, issues, or pull requests.
* Other conduct which could reasonably be considered inappropriate in a
  professional setting

## Enforcement Responsibilities

Community leaders are responsible for clarifying and enforcing our standards of
acceptable behavior and will take appropriate and fair corrective action in
response to any behavior that they deem inappropriate, threatening, offensive,
or harmful.

Community leaders have the right and responsibility to remove, edit, or reject
comments, commits, code, wiki edits, issues, and other contributions that are
not aligned to this Code of Conduct, and will communicate reasons for moderation
decisions when appropriate.

## Scope

This Code of Conduct applies within all community spaces, and also applies when
an individual is officially representing the community in public spaces.
Examples of representing our community include using an official e-mail address,
posting via an official social media account, or acting as an appointed
representative at an online or offline event.

## Enforcement

Instances of abusive, harassing, or otherwise unacceptable behavior may be
reported to the community leaders responsible for enforcement at conduct@metamask.io.
All complaints will be reviewed and investigated promptly and fairly.

All community leaders are obligated to respect the privacy and security of the
reporter of any incident.

## Enforcement Guidelines

Community leaders will follow these Community Impact Guidelines in determining
the consequences for any action they deem in violation of this Code of Conduct:

### 1. Correction

**Community Impact**: Use of inappropriate language or other behavior deemed
unprofessional or unwelcome in the community.

**Consequence**: A private, written warning from community leaders, providing
clarity around the nature of the violation and an explanation of why the
behavior was inappropriate. A public apology may be requested.

### 2. Warning

**Community Impact**: A violation through a single incident or series
of actions.

**Consequence**: A warning with consequences for continued behavior. No
interaction with the people involved, including unsolicited interaction with
those enforcing the Code of Conduct, for a specified period of time. This
includes avoiding interactions in community spaces as well as external channels
like social media. Violating these terms may lead to a temporary or
permanent ban.

### 3. Temporary Ban

**Community Impact**: A serious violation of community standards, including
sustained inappropriate behavior.

**Consequence**: A temporary ban from any sort of interaction or public
communication with the community for a specified period of time. No public or
private interaction with the people involved, including unsolicited interaction
with those enforcing the Code of Conduct, is allowed during this period.
Violating these terms may lead to a permanent ban.

### 4. Permanent Ban

**Community Impact**: Demonstrating a pattern of violation of community
standards, including sustained inappropriate behavior,  harassment of an
individual, or aggression toward or disparagement of classes of individuals.

**Consequence**: A permanent ban from any sort of public interaction within
the community.

## Attribution

This Code of Conduct is adapted from the [Contributor Covenant][homepage],
version 2.0, available at
https://www.contributor-covenant.org/version/2/0/code_of_conduct.html.

Community Impact Guidelines were inspired by [Mozilla's code of conduct
enforcement ladder](https://github.com/mozilla/diversity).

[homepage]: https://www.contributor-covenant.org

For answers to common questions about this code of conduct, see the FAQ at
https://www.contributor-covenant.org/faq. Translations are available at
https://www.contributor-covenant.org/translations.

# Security Policy##
@Edgarruiz856
## Responsible Disclosure Security Policy
by Edgar Manuel Ruiz Arias 
A responsible disclosure policy helps protect users of the project from publicly disclosed security vulnerabilities without a fix by employing a process where vulnerabilities are first triaged in a private manner, and only publicly disclosed after a reasonable time period that allows patching the vulnerability and provides an upgrade path for users.

When contacting us directly via email, we will do our best efforts to respond in a reasonable time to resolve the issue. When contacting a security program their disclosure policy will provide details on time-frame, processes and paid bounties.

We kindly ask you to refrain from malicious acts that put our users, the project, or any of the project's team members at risk.

## Reporting a Security Issue

We consider the security of our systems a top priority. But no matter how much effort we put into system security, there can still be vulnerabilities present.

If you discover a security vulnerability, please use one of the following means of communications to report it to us:

- Report the security issue on our [MetaMask HackerOne](https://hackerone.com/metamask) program.

For further questions about our security program please visit the [MetaMask Security Program](https://metamask.io/security/) page.

Your efforts to responsibly disclose your findings are sincerely appreciated and will be taken into account to acknowledge your contributions.

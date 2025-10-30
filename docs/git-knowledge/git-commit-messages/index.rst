Git: Commit Messages Guide
===========================

Complete guide to writing effective Git commit messages using conventional commits format for better collaboration and automation.

.. contents:: Table of Contents
   :local:
   :depth: 2

Overview
--------

Writing clear and consistent commit messages is essential for maintaining a clean Git history and enabling automated tooling. This guide covers two approaches:

- **Normal Git Commit Messages** - Free-form, casual approach
- **Formatted Git Commit Messages** - Structured conventional commits format

Reference Documentation
~~~~~~~~~~~~~~~~~~~~~~~

- `EU Component Library - Git Conventions <https://ec.europa.eu/component-library/v1.15.0/eu/docs/conventions/git/>`_

Normal Git Commit Messages
---------------------------

Normal commit messages are free-form and casual, with no specific structure or rules.

Example
~~~~~~~

.. code-block:: text

    Added product helper

Characteristics
~~~~~~~~~~~~~~~

- Free-form and casual
- No rules or structure
- Typically short, not standardized
- Harder to automate parsing or generate changelogs

Pros
~~~~

- Quick and easy for solo or small projects
- No learning curve

Cons
~~~~

- Lacks consistency across commits
- Doesn't communicate purpose clearly (is it a fix, a feature, or a refactor?)
- Hard to automate tooling (like changelogs or semantic versioning)

Formatted Git Commit Messages (Conventional Commits)
-----------------------------------------------------

Conventional Commits is a specification that provides a standardized format for commit messages, making them easier to read, parse, and automate.

Commit Message Format Structure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The commit message consists of three parts:

1. **Header** (mandatory)
2. **Body** (optional)
3. **Footer** (optional)

Syntax
~~~~~~

.. code-block:: text

    <type>(<scope>): <subject>
    <BLANK LINE>
    <body>
    <BLANK LINE>
    <footer>

Rules
~~~~~

- The header is mandatory and the scope is optional
- Any line of the commit message cannot be longer than **100 characters**
- This allows the message to be easier to read on GitHub as well as in various git tools

Header Structure
----------------

The header has a special format that includes a type, an optional scope, and a subject:

.. code-block:: text

    <type>(<scope>): <subject>

Type
~~~~

The type defines what kind of change is this. See :ref:`commit-types` for complete list.

Scope
~~~~~

The scope is optional but helpful! It defines what part of the codebase the change affects.

Examples:

.. code-block:: text

    feat(cart): add discount coupon logic
    fix(product): wrong price calculation
    chore(deps): update composer packages

Subject
~~~~~~~

The subject is required and should follow these rules:

- Use **imperative mood** (like giving a command): "add" not "added"
- Keep it under **50-70 characters**
- **Capitalize** the first word
- **No period** at the end

Good Example:

.. code-block:: text

    feat(checkout): add scan credit card button

Bad Example:

.. code-block:: text

    Added scan credit card button.

Body
----

The body is optional but great for providing context.

Use it to explain:

- **Why** the change was made
- **How** it solves a problem
- Any additional context

Example:

.. code-block:: text

    This adds a modal popup to scan the user's credit card using the webcam.
    We're using BlinkCard SDK and filling values via JS for UX improvement.

Footer
------

The footer is optional and used for:

- Breaking changes
- Issue references

Example:

.. code-block:: text

    BREAKING CHANGE: Checkout page structure changed to support scan feature.

    Closes #123

.. _commit-types:

Commit Types
------------

Common commit types and their purposes:

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Type
     - Description
   * - ``feat``
     - A new feature
   * - ``fix``
     - A bug fix
   * - ``docs``
     - Documentation only changes
   * - ``style``
     - Changes that do not affect the meaning of the code (white space, formatting, missing semi-colons, etc)
   * - ``refactor``
     - A code change that neither fixes a bug nor adds a feature
   * - ``perf``
     - A code change that improves performance
   * - ``test``
     - Adding missing tests
   * - ``chore``
     - Changes to the build process or auxiliary tools and libraries, such as documentation generation

Examples
--------

Type 1: feat - A New Feature
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    feat(user-auth): implement two-factor authentication

    Added support for two-factor authentication (2FA) in the login process. Users can now enable 2FA via their account settings.

    - Integrated with Google Authenticator
    - Requires users to enter a 6-digit code after entering their password

    Closes #101

Type 2: fix - A Bug Fix
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    fix(cart): resolve issue with item quantity not updating correctly

    Fixed a bug where the cart quantity did not update when the user modified the quantity through the cart page.

    - Updated the cart item model to trigger re-calculation on quantity change
    - Added unit tests for this behavior

    Fixes #87

Type 3: docs - Documentation Only Changes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    docs: update README with setup instructions for local environment

    Added instructions for setting up the project on a local machine, including dependencies and configuration steps.

    - Added section for Docker setup
    - Updated prerequisites for running the project locally

    Related to #112

Type 4: style - Code Formatting Changes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    style(css): format spacing in main.scss

    Reformatted the `main.scss` file to improve readability and consistency in indentation.

    - Added consistent indentation (2 spaces)
    - Removed unnecessary trailing spaces

    No functional changes

Type 5: refactor - Code Refactoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    refactor(auth): simplify login flow and remove deprecated code

    Refactored the login module to streamline the user authentication process. Removed old code that was no longer used in the flow.

    - Replaced old login validation with newer, more secure method
    - Removed legacy methods and imports

    BREAKING CHANGE: Removed deprecated methods in `AuthService`

Type 6: perf - Performance Improvements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    perf(query): optimize SQL query for fetching recent orders

    Improved the performance of the SQL query used to fetch recent orders by indexing the `order_date` column and refactoring the WHERE clause.

    - Reduced query execution time from 500ms to 100ms
    - Added new index to `order_date` column

    Related to performance review task #134

Type 7: test - Adding Tests
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    test(user-profile): add unit tests for profile update validation

    Added unit tests to cover validation logic for the user profile update form.

    - Added tests for required fields, email validation, and password strength
    - Increased code coverage by 20%

    Refs #108

Type 8: chore - Build Process and Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    chore(deps): upgrade eslint to v7.0

    Upgraded `eslint` to version 7.0 and updated associated configuration to meet the new rules.

    - Fixed deprecated rule usage in eslint configuration
    - Updated `.eslintrc.json` to match the latest recommended settings

    BREAKING CHANGE: Projects using older eslint configs may fail linting

Writing Commit Messages
-----------------------

Step-by-Step Process
~~~~~~~~~~~~~~~~~~~~

#. Stage your changes:

   .. code-block:: bash

       git add .

#. Start the commit:

   .. code-block:: bash

       git commit

#. The default editor will open (usually vim or nano)

#. Write your commit message following the conventional commits format

#. Save and close the editor

Quick Commit (One-Liner)
~~~~~~~~~~~~~~~~~~~~~~~~~

For simple commits, you can use the ``-m`` flag:

.. code-block:: bash

    git commit -m "feat(checkout): add scan credit card button"

Multi-Line Commit Message
~~~~~~~~~~~~~~~~~~~~~~~~~

For detailed commits with body and footer:

.. code-block:: bash

    git commit -m "feat(checkout): add scan credit card button" \
        -m "This adds a modal popup to scan the user's credit card using the webcam." \
        -m "We're using BlinkCard SDK and filling values via JS for UX improvement." \
        -m "Closes #123"

Or simply use ``git commit`` without ``-m`` to open the editor and write a multi-line message.

Best Practices
--------------

Do's
~~~~

- Use imperative mood in the subject line ("add" not "added")
- Keep the subject line under 70 characters
- Capitalize the first word of the subject
- Do not end the subject with a period
- Use the body to explain "what" and "why" vs. "how"
- Reference issues and pull requests when applicable
- Use breaking change notation when appropriate

Don'ts
~~~~~~

- Don't write vague commit messages like "fix bug" or "update code"
- Don't mix multiple concerns in a single commit
- Don't write commit messages longer than 100 characters per line
- Don't use past tense ("added feature") use imperative ("add feature")
- Don't skip the body when the commit needs explanation

Comparison: Normal vs Formatted Commits
----------------------------------------

Normal Commits Pros
~~~~~~~~~~~~~~~~~~~

- Quick and easy for solo or small projects
- No learning curve

Normal Commits Cons
~~~~~~~~~~~~~~~~~~~

- Lacks consistency across commits
- Doesn't communicate purpose clearly
- Hard to automate tooling (like changelogs or semantic versioning)

Formatted Commits Pros
~~~~~~~~~~~~~~~~~~~~~~

- Highly descriptive and consistent
- Easier for team collaboration
- Allows use of automated tools (e.g., auto-changelog, semantic versioning)
- Makes reviewing Git history cleaner
- Enables automated release notes generation

Formatted Commits Cons
~~~~~~~~~~~~~~~~~~~~~~

- Slight learning curve
- Requires some discipline or tooling (like commit hooks or linters)

Automation Tools
----------------

Using conventional commits enables various automation tools:

- **Semantic Versioning** - Automatically determine version bumps
- **Changelog Generation** - Auto-generate changelogs from commits
- **Release Notes** - Generate release notes automatically
- **Commit Hooks** - Validate commit message format
- **CI/CD Integration** - Trigger different workflows based on commit type

Example Tools
~~~~~~~~~~~~~

- `commitlint <https://commitlint.js.org/>`_ - Lint commit messages
- `semantic-release <https://semantic-release.gitbook.io/>`_ - Automated version management
- `standard-version <https://github.com/conventional-changelog/standard-version>`_ - Generate changelogs

See Also
--------

- :doc:`../git-first-time-setup/index` - First time Git configuration
- :doc:`../git-stash/index` - Git stash guide
- :doc:`../git-line-endings/index` - Fix Git line ending issues
- `Conventional Commits Specification <https://www.conventionalcommits.org/>`_


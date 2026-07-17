# Contributing to Bedrock Horizons

Please read this guide before contributing.

---

# Before You Begin

Before opening an issue or pull request, please:

- Read the README.
- Read the Code of Conduct.
- Search existing Issues and Pull Requests to avoid duplicates.
- Ensure you understand the project's licensing model.

---

# Ways to Contribute

There are many ways to contribute to Bedrock Horizons, including:

- Bug fixes
- Performance improvements
- Visual enhancements
- Lighting improvements
- Fog improvements
- Water improvements
- Color grading adjustments
- Documentation improvements
- Testing on different platforms
- Feature suggestions
- Localization
- Code cleanup and refactoring

Not every contribution has to involve writing code.

---

# Development Guidelines

## Code

When contributing source code:

- Follow the existing project structure.
- Keep changes focused on a single purpose.
- Avoid unrelated formatting changes.
- Write clear and descriptive commit messages.
- Test your changes before submitting.

Whenever possible, keep pull requests small and easy to review.

---

## JSON Files

Most of Bedrock Horizons is built using JSON.

Please ensure that:

- Files remain properly formatted.
- Indentation is consistent with the rest of the project.
- Object ordering is preserved where practical.
- File names follow the existing naming conventions.
- Identifiers use the existing `bh:` namespace.

Example:

```json
{
  "description": {
    "identifier": "bh:forest_fog"
  }
}
```

---

## Visual Assets

When contributing textures or artwork:

- Maintain the existing visual style.
- Keep resolutions consistent.
- Avoid unnecessary file size increases.
- Test assets in-game before submitting.

Do not submit copyrighted assets that you do not own or have permission to distribute.

---

# Testing

Before submitting a pull request, verify that:

- The project loads successfully.
- Minecraft reports no content errors.
- New visuals behave as expected.
- Existing functionality has not been broken.
- Performance remains reasonable.

If possible, test on multiple devices or platforms.

---

# Commit Messages

Write concise, descriptive commit messages.

Good examples:

```git commit message
Improve snowy biome lighting

Fix swamp fog transition

Add color grading for Pale Garden

Optimize cloud texture loading

Update README documentation
```

Avoid vague messages such as:

```git commit message
Update

Fix stuff

Changes

Testing
```

---

# Pull Requests

When submitting a pull request:

- Explain what the change does.
- Describe why the change is needed.
- Reference related issues if applicable.
- Include screenshots for visual changes whenever possible.
- Keep discussions professional and constructive.

Large pull requests may take longer to review.

---

# Reporting Bugs

When opening a bug report, include as much information as possible, including:

- Minecraft version
- Platform (Windows, Android, iOS, Xbox, etc.)
- Steps to reproduce
- Expected behavior
- Actual behavior
- Screenshots or videos, if applicable
- Any content log errors

The more information provided, the easier it is to investigate.

---

# Feature Requests

Feature requests are welcome.

Please explain:

- The problem you are trying to solve.
- Your proposed solution.
- Any alternatives you considered.
- Why the feature would benefit the project.

Not every request will be accepted, but all constructive suggestions are appreciated.

---

# Licensing

By submitting a contribution to Bedrock Horizons, you confirm that:

- You created the work yourself, or have the legal right to contribute it.
- Your contribution may be distributed under the project's licenses.

Project licensing:

| Content | License |
| ------- | ------- |
| Source Code | Mozilla Public License 2.0 (MPL-2.0) |
| Textures, Artwork, and Other Assets | Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0) |

---

# Questions

If you have questions before contributing, feel free to open a GitHub Discussion or Issue.

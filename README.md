# SafeGen Documentation

This repository hosts the public documentation site for **SafeGen**, a parental-control platform that enforces age-appropriate access across digital platforms.

## Table of Contents
- [About SafeGen](#about-safegen)
- [Repository Layout](#repository-layout)
- [Local Preview](#local-preview)
- [Contributing Content](#contributing-content)
- [Data Rooms](#data-rooms)
- [Support](#support)

## About SafeGen
SafeGen helps organizations comply with online safety regulations by providing identity verification, age checks, and granular parental controls. This repository collects the static documentation that explains how SafeGen works, how to integrate it, and how we manage reference materials for partners.

## Repository Layout
- `index.html` – Landing page for the documentation site.
- `dataroom/` – Structured reference packs for partners and auditors. See [Data Rooms](#data-rooms) for details.
- `README.md` – You are here.

## Local Preview
The documentation is a static site. To preview it locally:

```bash
# From the repository root
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser. Any changes to HTML or Markdown files will be reflected on refresh.

## Contributing Content
1. Create or update Markdown/HTML content within the relevant folder.
2. Keep navigation links current so new pages are discoverable from `index.html` or the corresponding section index.
3. Run the [local preview](#local-preview) to verify links and formatting.
4. Open a pull request describing the change and include screenshots for visual updates when possible.

## Data Rooms
The `dataroom/` directory contains focused packages for specific partners. Each data room includes its own README that outlines available assets and access notes. For example, the [CarbonKilos data room](dataroom/carbonkilos/README.md) contains integration artifacts tailored to that partnership.

## Support
If you have questions or need to report an issue, open a GitHub issue or contact the SafeGen documentation team.

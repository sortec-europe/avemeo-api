# Contributing

Thanks for helping improve the documentation of the Avemeo REST API and AI connector. Corrections, clarifications, new use cases and translations are welcome.

## Ways to contribute

- **Found an error or something unclear?** [Open an issue](https://github.com/sortec-europe/avemeo-api/issues/new/choose) using the *Documentation issue* template.
- **Have a question about the API or the connector?** Use the *Question* template or write to [avemeo@sortec.sk](mailto:avemeo@sortec.sk).
- **Want to fix it yourself?** Fork the repository, edit the Markdown and open a pull request.

## Guidelines

- **Keep facts verifiable.** Only document behaviour you have observed on an Avemeo cloud or that the Avemeo team has confirmed. Mark planned functionality clearly as *planned* or *in development*.
- **Keep all languages in sync.** Most pages exist in English (`docs/`, `README.md`), Slovak (`docs/sk/`, `README.sk.md`) and Czech (`docs/cs/`, `README.cs.md`). If you change one, change the others or say in the pull request that the translations are still needed.
- **No technical API details.** Endpoints, headers, request and response formats and code examples of the Avemeo API are not published in this repository – the API documentation is provided by Avemeo to customers and integrators individually. Anything beyond a high-level description needs the Avemeo team's approval.
- **No secrets.** Never include tokens, passwords, API keys, device tokens or personal data – not even in examples. Use placeholders such as `<token>` or `YOUR_USER`.
- **No customer data.** Use generic names (for example *Main Street store*, *room 204*) rather than real customers, device IDs or screen names from production accounts.
- **Style:** short sentences, one idea per paragraph, tables for structured facts, code blocks for anything a reader will copy. Headings should say what the section is about so that people and search engines can find it.
- **Links:** use relative links inside the repository and check that they resolve.
- **Changelog:** add a line to [CHANGELOG.md](CHANGELOG.md) for anything a reader would notice.

## Pull request checklist

- [ ] Facts verified; planned functionality marked as such
- [ ] English, Slovak and Czech versions updated (or the gap noted)
- [ ] No secrets, tokens or customer data
- [ ] Internal links work
- [ ] CHANGELOG.md updated

## License

By contributing you agree that your contribution is licensed under [CC BY 4.0](LICENSE), like the rest of the documentation.

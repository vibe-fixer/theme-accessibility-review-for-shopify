# Theme accessibility review for Shopify: a free Claude skill by VibeFix (vibe-fixer.com)

A free Claude skill and copy-paste prompt that reviews one Shopify theme Liquid file (a section, snippet or block) for accessibility problems you can see in the source, and suggests a Liquid, HTML or CSS fix for each one.

It checks five things:

1. **Form fields have labels.** Inputs, selects and textareas with no `<label>`, `aria-label` or `aria-labelledby`. A placeholder alone is flagged.
2. **Images have alt text.** `<img>` with no `alt`, and `image_tag` output that relies on alt text the merchant may never have filled in.
3. **Links and buttons have a name.** Icon-only cart, search, social, close and arrow controls with nothing a screen reader can read out, and hidden labels that don't match the visible text.
4. **Keyboard focus.** `outline: none` with no replacement focus style, `tabindex` above 0, clickable `<div>`s, and `aria-hidden` on things you can tab to.
5. **Colour contrast, where both colours are written in the file.** It computes the ratio. Colours that come from theme settings can't be known from the source, so it lists them under "could not check" and does not guess.

Each finding comes with the line number, the WCAG 2.1 success criterion and level, whether it **Fails** (the source shows it) or needs a **Check** (it depends on something the file can't show), and the smallest code change that fixes it, using your theme's own `visually-hidden` class and translation keys.

## Install

### Claude Code

```
claude plugin marketplace add vibe-fixer/theme-accessibility-review-for-shopify
claude plugin install theme-accessibility-review-for-shopify@vibe-fixer-a11y
```

Then, in your theme folder: *"Review sections/footer.liquid for accessibility."*

### Claude.ai (web and desktop)

Download the [`skills/theme-accessibility-review-for-shopify`](skills/theme-accessibility-review-for-shopify) folder and zip it, so the folder (not the SKILL.md alone) is at the top of the zip. In Claude, open **Customize → Skills**, press **+**, then **Create skill → Upload a skill**, and choose the zip. Skills need code execution turned on under **Settings → Capabilities**.

### Any AI chat

Tested in Claude. Copy [`prompt/review-prompt.md`](prompt/review-prompt.md) into a new chat and paste your `.liquid` file at the end.

## Try it

[`examples/broken-newsletter.liquid`](examples/broken-newsletter.liquid) is a small section with planted problems. In our test (25 Nov 2026) the skill found all 8 planted failures: faint text, a removed focus outline, a placeholder-only email field, an icon-only submit button, a clickable `<div>`, an icon-only Instagram link, `tabindex="3"`, and an image-only cart link. It also flagged the image with no `alt:` as a Check. On Dawn's `sections/footer.liquid` it reported 0 Fails and 2 Checks (both about merchant-supplied alt text).

## What it does not do

- It reads one file's source. It doesn't open your store, run your JavaScript or see your theme settings, so it finds some issues, not all.
- It doesn't test WCAG 2.2-only criteria such as target size.
- It doesn't make a store "compliant", and it isn't legal advice.

Check every change in the theme editor preview before you publish, and test with a keyboard and a screen reader.

## Want it done for you?

VibeFix's [free Shopify homepage accessibility checker](https://vibe-fixer.com/tools/shopify-accessibility-checker?src=gh-a11y-skill) checks your live homepage, read-only, in about a minute. If it finds issues, VibeFix's AI agent can fix them in your theme's code on an unpublished copy that you preview and publish yourself, then re-check your live store. Details: [vibe-fixer.com/stores](https://vibe-fixer.com/stores?src=gh-a11y-skill).

## License

MIT. Product names are used only to describe compatibility; VibeFix is not affiliated with Shopify.

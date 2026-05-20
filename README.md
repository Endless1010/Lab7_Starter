# Lab 7 - Bowen Wu

## Check Your Understanding

**1) Where would you fit your automated tests in your Recipe project development pipeline? Select one of the following and explain why.**

Within a GitHub Action that runs whenever code is pushed.

I'd put them in CI so they run on every push. If you only run tests manually before pushing, people forget, especially when you're rushing to finish something. And if you wait until all the development is done, you end up with a pile of bugs stacked on top of each other and it's way harder to figure out which change broke what. Running on every push catches stuff early when it's still easy to fix.

**2) Would you use an end to end test to check if a function is returning the correct output? (yes/no)**

No. E2E tests are for simulating actual user behavior in the browser, like clicking buttons and navigating between pages. They're slow and kind of overkill for checking what a single function returns. A unit test does that way faster and tells you exactly which function is broken.

**3) What is the difference between navigation and snapshot mode?**

Navigation mode reloads the page and measures everything from a cold load, so you get metrics like First Contentful Paint and Largest Contentful Paint. Snapshot mode just looks at the page in whatever state it's already in without reloading. So navigation is good for performance numbers, while snapshot is more useful for things like accessibility checks on the current DOM (for example, checking a modal after you've opened it).

**4) Name three things we could do to improve the CSE 110 shop site based on the Lighthouse results.**

1. Add a `lang` attribute to the `<html>` tag. Lighthouse flagged this under Accessibility. Without it, screen readers don't know what language to pronounce things in. Setting `<html lang="en">` fixes it.

2. Add a meta description. Lighthouse flagged this under SEO. There's no `<meta name="description">` on the page, so search engines have nothing to show in the result snippet. Adding a short description of the shop would help.

3. Use longer cache lifetimes for static assets. Lighthouse said the icons, JS, and CSS only have a 10 minute cache TTL, which means returning visitors keep re-downloading files that haven't changed. Bumping `Cache-Control` max-age to something longer on `shop-icon.png`, `main.js`, `product-item.js`, `storage.js`, and `main.css` would make repeat visits faster.

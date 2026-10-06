# Image assets still to drop in

The INTI × BeLive Nilai page (`index.html`) is fully wired, but the photography for
the two Nilai residences is not in the repo yet. Any file listed below that is
missing renders as a tidy "Photo coming soon" panel (or, for the route guides and
the partnership photo, the block hides itself), so the page never shows a broken
image. Drop a file in at the repo root with the exact name and it appears — no
code change needed.

## Campus / partnership

| File | Where it appears | Status |
| --- | --- | --- |
| `INTI-campus.jpg` | Hero background (INTI Nilai campus photo) | in repo — only 680x454, so a higher-resolution original would render sharper |
| `BeLivexINTI_photo.jpg` | "Built Together with INTI" partnership card | still needed |

## Youth City Residence

| File | Where it appears | Status |
| --- | --- | --- |
| `YouthCity_condo.jpg` | Building photo on the Youth City tab | in repo |
| `YC_pool.jpg`, `YC_gym.jpg`, `YC_playground.jpg` | Facility strip | in repo |
| `YC_master.jpg`, `YC_double_1.jpg` (RM878), `YC_double_2.jpg` (RM678) | Room cards | in repo |
| `YC_kitchen.jpg`, `YC_dining.jpg`, `YC_yard.jpg` | Shared spaces | in repo |
| `BeLive_YouthCity_INTI.jpg` | "Getting to INTI International University" route guide | still needed |

## Akasia @ Bandar Belia

| File | Where it appears | Status |
| --- | --- | --- |
| `Akasia_condo.jpg` | Building photo on the Akasia tab | in repo |
| `AK_pool.jpg`, `AK_gym.jpg`, `AK_playground.jpg` | Facility strip | in repo |
| `AK_master.jpg`, `AK_double.jpg`, `AK_single.jpg` | Room cards | in repo |
| `AK_kitchen.jpg`, `AK_living.jpg`, `AK_yard.jpg` | Shared spaces | in repo |
| `BeLive_Akasia_INTI.jpg` | "Getting to INTI International University" route guide | still needed |

## Logo

`inti-logo.png` is INTI's official International University & Colleges lockup
(2000x433, transparent, with the "Your Future Built Today" bar). It is used in
the nav, the partnership card and the footer. Because the type is black and
grey, the footer places it on a white plaque rather than recolouring the mark.

## Deployment

**Live at <https://karenwong-png.github.io/inti/>.**

Pages is enabled and serves from the `gh-pages` branch.
`.github/workflows/deploy-pages.yml` runs on every push to `main` and pushes
`main`'s tree onto `gh-pages`; GitHub serves it from there. No manual step.

### Why it publishes this way

The workflow originally used the `configure-pages` / `upload-pages-artifact` /
`deploy-pages` trio with `enablement: true`. That can never work from a
workflow: creating a Pages site is not available to the workflow token
("Resource not accessible by integration"), only to a repo admin. Pages was
enabled instead by pushing a `gh-pages` branch, which GitHub auto-enables
Pages for. With Pages sourced from a branch, GitHub locks the `github-pages`
environment to that branch, so a `deploy-pages` job running on `main` is
rejected with "Branch main is not allowed to deploy to github-pages due to
environment protection rules" — hence the plain push.

If the source is ever switched to **GitHub Actions** (Settings → Pages →
Build and deployment), the workflow can go back to the artifact trio, minus
the `enablement` flag.

### Custom domain — not set

There is deliberately no `CNAME` file. `inti.belive.my` currently resolves to
**Vercel** (as does `inceif.belive.my`), so a `CNAME` claiming it for Pages
would only make GitHub flag the domain as misconfigured and redirect the
working github.io URL at a host that serves something else.

To move the domain to Pages later: add a root `CNAME` file containing
`inti.belive.my`, and in Cloudflare change the `inti` record from the Vercel
target to a `CNAME` at `karenwong-png.github.io`, DNS-only (grey cloud) until
GitHub has issued the certificate.

# Astro v6 + Cloudflare + middleware + `nodejs_compat` leads to wrong output on SSR pages. 

## Summary

* Astro v6-beta project 
* ...with the Cloudflare adapter
* ...with `"compatibility_flags": ["nodejs_compat"]` in `wrangler.jsonc`
* ...with any middleware (even a minimal `return next()`) 

...leads to SSR pages showing as `[object Object]` in the browser *in preview mode and in deployment to CF only* (`dev` mode is unaffected.)


## Steps to reproduce

1. Clone this repository.
2. Install dependencies with `pnpm install`.
5. Test the application: `pnpm run preview`.


### Expected behaviour

The application should display the word __"Astro"__, as per the minimal template.


### Actual behaviour

The page displays `[object Object]`.


## Other notes

If you delete or rename `src/middleware.ts`, the page displays normally.

If you edit `wrangler.jsonc` to remove the line `"nodejs_compat",`, the page displays normally.

I've checked every other combination of v5/v6-beta and node/cloudflart adapter and it's only the exact combination of v6-beta/cloudflare that generates this behaviour.

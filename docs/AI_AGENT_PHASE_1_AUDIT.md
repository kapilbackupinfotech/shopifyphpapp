# AI Voice & Chat Agent — Phase 1 Repository Audit

## Repository
- Repository: kapilbackupinfotech/shopifyphpapp
- Branch: ai-agent/phase-1-foundation
- Base: main

## Existing foundation
- Laravel backend under web/
- Existing Shopify OAuth and callback routes
- Existing Shopify webhook registration/processing
- Existing persisted Shopify sessions
- React frontend is currently a Git submodule
- Shopify CLI PHP app template structure

## Important compatibility findings
1. The current backend is Laravel 8.x, while the target architecture requires Laravel 12.
2. The current Composer dependency uses shopify/shopify-api ^5.0. Shopify now marks this package deprecated and recommends shopify/shopify-app-php.
3. Existing authentication code uses the older Shopify PHP library API, so upgrading the framework/library must be treated as a controlled migration rather than a drop-in dependency bump.
4. The current app has product-demo/template routes and should not have those replaced blindly.

## Phase 1 implementation plan
1. Upgrade the backend foundation to the Laravel 12 / PHP 8.2+ baseline in a controlled migration.
2. Adopt Shopify's maintained PHP app package and current embedded-app authentication flow.
3. Preserve existing session data and OAuth behavior during migration.
4. Introduce an explicit shops tenant record and shop-scoped settings.
5. Add secure OAuth token storage metadata and webhook subscription tracking.
6. Add a first dashboard endpoint/UI shell that resolves the authenticated shop server-side.
7. Add AI provider configuration placeholders without exposing secrets to React/storefront.
8. Add automated tests for tenant resolution and authenticated shop isolation.
9. Run composer validation, migrations, PHPUnit, frontend build, and Shopify CLI checks before declaring Phase 1 complete.

## Security baseline
- Never trust shop_id from the browser.
- Resolve merchant identity from authenticated Shopify context.
- Keep API secrets server-side.
- Request only Shopify scopes required by implemented functionality.
- Keep AI provider code behind services/interfaces.
- Do not add RAG, voice, commerce actions, or billing until the Phase 1 foundation is verified.

## Current status
Phase 1 repository inspection is complete. The branch is intentionally isolated from main. The Laravel 8 -> Laravel 12 and Shopify PHP library migration is the first implementation dependency; proceeding by simply adding Phase 1 models to the legacy foundation would create an inconsistent production architecture.

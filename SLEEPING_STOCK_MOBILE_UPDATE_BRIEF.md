# Sleeping Stock Mobile — Web Update Brief

## Updated

- Renamed the web companion module from **NMTS Mobile** to **Sleeping Stock Mobile**.
- Added the new route: `/sleeping-stock-mobile`.
- Kept `/nmts-mobile` as a compatibility redirect.
- Added a Device Pairing section to the web page.
- Pairing requires all three values:
  - Brand
  - Dealer
  - Branch Code
- The Generate Pairing Code button remains disabled until all three values are selected.
- Missing fields are listed clearly in the validation message.
- Added backend validation so frontend validation cannot be bypassed.
- Added validation that the selected Brand, Dealer and Branch combination exists and is within the logged-in user's permitted scope.
- Added a one-time pairing code API with a 10-minute expiry.
- Added pairing verification API that creates an active device mapping and prevents reuse of the pairing code.
- Existing mobile device list, activate/block/remove, stock search and perpetual stock APIs were retained.
- App information now returns the name **Sleeping Stock Mobile**.
- Branch scope API now includes `code` when a branch code exists; otherwise branch name is used as the pairing value.

## New Backend APIs

- `POST /api/mobile/pairing`
- `POST /api/mobile/pairing/verify`

## Verification

- Backend Python syntax compilation passed.
- Frontend source was reviewed for route and naming consistency.
- A full React production build could not be run because `node_modules` was intentionally not included in the uploaded project. Run `npm install` and `npm run build` in the frontend folder.

## Configuration

Optional environment variables:

- `SLEEPING_STOCK_MOBILE_VERSION`
- `SLEEPING_STOCK_MOBILE_APK_URL`

Old `NMTS_MOBILE_VERSION` and `NMTS_MOBILE_APK_URL` values remain supported as fallbacks.

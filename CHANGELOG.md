# Changelog

Summary of the main changes. Current version: **0.4.6**

## 0.4.x – Offer calculator & polish

- Premium / discount can be entered in **%**, **sats** or **BTC**
- Both calculator modes show the same results in the same order: premium in %, in currency and in sats first, then the amount you receive (with the BTC value below it), sats at market price, offer price and market price
- Thousands separators in all amount fields and results
- Price tiles are shown two per row (also in the app); the font scales with the card width
- Narrow cards (phone, app) no longer overflow; result values never wrap

## 0.3.x – Stability

- Currencies can be reordered in the editor
- Inputs are remembered in the browser, also after a dashboard reload or a refresh of the editor preview
- The selected currency and input field stay correct when currencies are removed or reordered
- In the sections view the card sizes itself, so the results are no longer cut off

## 0.2.x – Languages & units

- English and German, following the Home Assistant language
- The Bitcoin field can be switched between **sats** and **BTC**
- Larger title and labels, fiat fields in their own row below the Bitcoin field

## 0.1.x – First version

- Live conversion between sats, BTC and any number of currencies from your own price sensors
- Current prices on top of the card
- Visual editor and live preview in the card picker
- Optional offer calculator: check the spread of an offer or calculate the sats for a given premium

# Ignite – Send money animation prototype

A clickable prototype of the animation that plays when money is sent from you to another Ignite user. On success, the sending screen morphs into the transaction receipt.

Built from the Figma file **IGN: Design File MVP-01**:
- Sending screen: node `654:30414`
- Receipt screen: node `654:30595`

## Files

| File | What it is |
|---|---|
| `index.html` | The whole prototype. All CSS, JS and the two avatar images are inline. |
| `README.md` | This file. |

Nothing else is needed. There is no build step and there are no dependencies.

## Deploy on Vercel

1. Put `index.html` and `README.md` at the root of a GitHub repo.
2. In Vercel, choose **Add New → Project** and import the repo.
3. Leave **Framework Preset** as **Other**, with no build command and no output directory.
4. Click **Deploy**.

Every push to the main branch redeploys automatically.

To preview locally, open `index.html` in a browser.

## How to use it

The prototype opens on the sending screen in the **pending** state.

| Control | What it does |
|---|---|
| **Server response** bar (bottom) | Simulates the server. Tap **Success** or **Failure**. Prototype only, not part of the design. |
| **Restart prototype** tab (left edge) | Goes back to the pending state. Keeps the current theme. |
| **Light mode / Dark mode** tab (right edge) | Switches the IGN semantic colours between Dark and Light. |

## The animation

**1. Pending (loops until the server responds)**
- Dots flow along an S-curve from your avatar to Jane's.
- Your avatar breathes gently.
- The pending state always shows for at least 1.2s, so fast responses don't flicker.

**2. Success**
- Your avatar squashes slightly, then a coin travels the path (900ms, ease-in-out).
- Jane bounces, a ring pulses out and a check badge appears.
- "Sending" changes to "Sent".

**3. Morph into the receipt (about 1s after success)**
- Shared elements move: Jane's avatar shrinks into the seal, and the amount glides to the centre.
- Everything else fades out.
- The receipt's text and detail rows stagger in.

**4. Failure**
- The coin stalls halfway and returns to you.
- The path turns to the error colour and your avatar shakes.
- An alert badge appears and the header changes to "Not sent".

**Reduced motion:** if the device has reduced motion turned on, the travel and flow animations are replaced with simple crossfades.

## Timing reference

| Moment | Duration | Easing |
|---|---|---|
| Dot flow (loop) | 600ms per cycle | linear |
| Anticipation squash | 140ms | ease-out |
| Coin travel (success) | 900ms | ease-in-out |
| Jane bounce | 480ms | ease-out |
| Morph, shared elements | 560ms | `cubic-bezier(0.77, 0, 0.175, 1)` |
| Receipt rows | 260ms each, 45ms apart | `cubic-bezier(0.23, 1, 0.32, 1)` |
| Coin out and back (failure) | 450ms + 500ms | ease-out, then ease-in-out |

## Colours

All colours come from the IGN **Semantic** collection, written as CSS variables named after the Figma variables (for example `icon/brand` becomes `--icon-brand`). The prototype controls and the Server response bar use their own fixed colours because they are testing tools, not part of the design.

## Open questions for design

1. **Data mismatch.** The Figma sending screen says KES 500 to Jane Wairimu, but the receipt says Ksh 4,230.00 to Lisa Wanjiru Mwende. The prototype uses KES 500 and Jane Wairimu on both.
2. **Currency format.** "KES 500" changes to "Ksh 500.00" during the morph. One format on both screens would read better.
3. **Seal.** The seal is a drawn stand-in, because the Figma seal is a raster image.
4. **Coin.** There is no coin component in the IGN Component Library yet.
5. **Failure copy.** "Not sent" and "Nothing left your account." are placeholders. There is no failure screen in Figma.
6. **M-Pesa rows.** "M-Pesa reference" and "Transfer type: M-Pesa" may not suit an Ignite-to-Ignite transfer.

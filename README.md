# SlickPickleNick Multiplatform Alerts

Version: v0.2.0 restart

This is a GitHub Pages-ready multiplatform alert overlay for OBS. It is designed to work immediately from a single browser source URL while still offering a customization dashboard for users who want detailed control.

## Files

```text
multiplatform-alerts/
├─ index.html
├─ overlay.html
├─ assets/
│  ├─ logos/
│  └─ sounds/
└─ README.md
```

## Default OBS URL

After uploading this folder to GitHub Pages, the default browser source can be used immediately:

```text
https://YOUR-USERNAME.github.io/YOUR-REPO/overlay.html
```

The default overlay connects to:

```text
ws://127.0.0.1:8080/
```

## Dashboard URL

Use the dashboard to customize the overlay and generate an OBS URL:

```text
https://YOUR-USERNAME.github.io/YOUR-REPO/index.html
```

The dashboard lets users adjust alert duration, transition speed, position, scale, fonts, sounds, platform colors, platform logos, event toggles, and action text templates.

## OBS Setup

1. Enable the Streamer.bot WebSocket server.
2. Confirm the WebSocket server is available at `ws://127.0.0.1:8080/` or update the URL in the dashboard.
3. Add a new OBS Browser Source.
4. Use `overlay.html` directly or copy the generated dashboard URL.
5. Set browser source dimensions to your canvas size, commonly `1920x1080`.
6. Recommended: check `Refresh browser when scene becomes active`.

The alert card itself is fixed at `750px × 300px` by default so it can stay consistently positioned across scenes.

## Streamer.bot Setup

No alert-specific sub-actions are required. The overlay connects to the Streamer.bot WebSocket server and sends a native `Subscribe` request for supported events.

Streamer.bot event simulations should fire through the same WebSocket event path as live events, so the overlay should respond to simulations when the matching platform/event is enabled.

## Supported Platforms and Events

### Twitch

- Follow
- Channel Point Redemption
- Automatic Reward Redemption
- Bits / Cheer
- Coin Cheer
- New / Prime Subscription
- Resubscription
- Gifted Subscription
- Community Gift
- Incoming Raid
- Charity Donation

### YouTube

- Subscribed
- Jewels Gifted
- Super Chat
- Super Sticker
- Membership Gift
- Gift Membership Received
- Member Milestone
- New Sponsor

### Kick

- Channel Reward Redemption
- Follow
- Gifted Kicks
- Gift Subscription
- Mass Gift Subscriptions
- Resubscription
- Subscription

### Fourthwall

- Donation
- Gift Purchase
- Order Placed
- Subscription Purchased

### Ko-Fi

- Commission
- Donation
- Resubscription
- Shop Order
- Subscription

### Pally.gg

- Campaign Tip

### Patreon

- Follow Created
- Pledge Created
- Pledge Updated

### StreamElements

- Tip

### Streamlabs

- Charity Donation
- Donation

### TipeeeStream

- Donation

### TreatStream

- Treat

## Images and Logos

Twitch, YouTube, and Kick alerts use a user profile image when Streamer.bot provides one and the platform setting is enabled.

When no profile image is available, the overlay uses the platform logo path from `assets/logos/`.

For platforms that do not support profile images in this overlay, the platform logo is always used.

You can replace the placeholder SVG files in `assets/logos/` with official logo files. Keep the same filenames or update the logo path in the dashboard.

## Sounds

The overlay includes three local sound files:

```text
assets/sounds/default-alert.wav
assets/sounds/soft-pop.wav
assets/sounds/sparkle.wav
```

The dashboard supports:

- Global sound
- Global volume
- Per-platform sound override
- Per-platform volume
- Custom relative path or URL

For best reliability, store sound files in `assets/sounds/` and reference them with a relative path.

## Action Text Templates

Templates support these tokens where Streamer.bot data is available:

```text
{amount}
{count}
{months}
{viewers}
{bits}
{reward}
{cost}
{recipient}
{tier}
{tierText}
```

Example:

```text
just resubscribed, and has been a sub for {months} months!
```

## Testing

The dashboard includes:

- Trigger Random Alert
- Per-event Test buttons
- Optional randomized preview loop

Streamer.bot's built-in event simulations should also trigger the overlay as long as the event is enabled and the browser source is connected to the WebSocket server.

## Notes

- The default overlay works with no query parameters.
- Customized OBS URLs store settings in the URL using an encoded config parameter.
- The alert card keeps a fixed bounding box by default and only scales visually if the scale setting is changed.

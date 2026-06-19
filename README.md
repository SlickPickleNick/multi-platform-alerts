# SlickPickleNick Multiplatform Alerts

Version: v0.2.1

This is a GitHub Pages-ready multiplatform alert overlay for OBS. The default `overlay.html` URL is intended to work immediately with a polished fixed design, while `index.html` provides a control-heavy dashboard for users who want customization.

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

The HTML files do not require a build step. Upload the files to a GitHub Pages repository and use the generated page URLs in OBS.

## Default OBS URL

After hosting the repo on GitHub Pages, the default browser source can be used immediately:

```text
https://YOUR-USERNAME.github.io/YOUR-REPO/overlay.html
```

The default overlay connects to Streamer.bot at:

```text
ws://127.0.0.1:8080/
```

## Dashboard URL

Use the dashboard to customize the overlay and generate a configured OBS URL:

```text
https://YOUR-USERNAME.github.io/YOUR-REPO/index.html
```

The dashboard can control alert duration, transition timing, time between alerts, position, scale, fixed dimensions, padding, gap, radius, image size, font sizes, sound behavior, platform colors, logo paths, event toggles, and action text templates.

## Default Alert Layout

The default alert card is designed around a fixed bounding box:

```text
Alert card: 740px × 190px
Internal padding: 20px
Image/logo box: 150px × 150px
Default position: center
```

The alert content is structured as:

```text
USERNAME
action text
```

There are no platform/event tags above the alert and no direct platform accent bar. Platform identity is shown through the gradient background and the profile image or platform logo.

The alert card keeps its bounding box fixed. Long usernames and action text are reduced in font size when needed so the content stays inside its assigned space.

## OBS Setup

1. Enable the Streamer.bot WebSocket server.
2. Confirm the WebSocket server is available at `ws://127.0.0.1:8080/`, or update the URL in the dashboard.
3. Add a new OBS Browser Source.
4. Use `overlay.html` directly, or copy the configured URL from `index.html`.
5. Set the browser source dimensions to your canvas size, commonly `1920x1080`.
6. Recommended: enable `Refresh browser when scene becomes active`.

## Streamer.bot Setup

No alert-specific sub-actions are required. The overlay connects to the Streamer.bot WebSocket server and sends a native `Subscribe` request for supported events.

Streamer.bot event simulations should fire through the same WebSocket event path as live events, so the overlay should respond to simulations when the matching platform/event is enabled and the OBS browser source is connected.

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

## Profile Images and Platform Logos

Twitch, YouTube, and Kick alerts use a user profile image when Streamer.bot provides one and the platform setting is enabled.

When no user profile image is available, or when the platform is not Twitch, YouTube, or Kick, the overlay uses the platform logo.

Logo files should be stored in:

```text
assets/logos/
```

Supported logo file types:

```text
.svg
.png
.webp
.jpg
.jpeg
.gif
.avif
```

The default logo paths are extensionless, such as:

```text
assets/logos/twitch
assets/logos/youtube
assets/logos/kick
assets/logos/fourthwall
assets/logos/kofi
assets/logos/pallygg
assets/logos/patreon
assets/logos/streamelements
assets/logos/streamlabs
assets/logos/tipeeestream
assets/logos/treatstream
```

When an extensionless path is used, the overlay automatically tries common image extensions. For example, `assets/logos/twitch` can resolve to `assets/logos/twitch.svg`, `assets/logos/twitch.png`, `assets/logos/twitch.webp`, and other supported formats.

You can also enter an exact logo file path in the dashboard, such as:

```text
assets/logos/twitch-purple.svg
assets/logos/kick.png
assets/logos/fourthwall.webp
```

If a logo cannot load, the overlay falls back to a text abbreviation inside the image box.

## Sounds

The overlay plays a sound when an alert appears, unless sounds are disabled or the OBS URL includes `mute=1`.

Recommended sound folder:

```text
assets/sounds/
```

Default sound path:

```text
assets/sounds/default-alert.wav
```

The dashboard supports:

- Global sound path
- Global volume
- Per-platform sound override
- Per-platform volume
- Custom relative paths or full URLs

Recommended sound formats are `.wav`, `.mp3`, and `.ogg`.

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
- Clear Preview Queue

Streamer.bot's built-in event simulations should also trigger the overlay as long as the event is enabled and the browser source is connected to the WebSocket server.

## Notes

- The default overlay works with no query parameters.
- Customized OBS URLs store settings in the URL using an encoded `config` parameter.
- The default visual style uses platform-colored gradients, not accent bars.
- The alert bounding box remains fixed by default to keep placement consistent across OBS scenes.

# SlickPickleNick Multiplatform Alerts

Version: `v0.1.1`

A GitHub Pages-hosted browser source alert system for Streamer.bot WebSocket events.

This overlay is designed for creators who want one alert system for multiple platforms without creating separate Streamer.bot subactions for every alert. The OBS browser source connects directly to the Streamer.bot WebSocket server, subscribes to supported events, queues alerts one at a time, and displays platform-specific alert cards.

---

## Files

```text
multiplatform-alerts/
├─ index.html      # Customization dashboard / Control Deck
├─ overlay.html    # OBS browser source overlay
└─ README.md       # Setup and event reference
```

---

## What This System Does

- Hosts from GitHub Pages.
- Uses one OBS browser source URL.
- Connects directly to Streamer.bot's WebSocket server.
- Subscribes to enabled Streamer.bot events automatically.
- Does not require event-specific Streamer.bot subactions.
- Queues alerts one at a time.
- Supports global alert duration and transition delay.
- Supports global sound and optional per-platform sound override.
- Supports platform-specific default colors with user color overrides.
- Uses the alert trigger username as the large headline.
- Uses the event action as smaller supporting text below the username.
- Removes platform/event tag labels from the visible alert card.
- Uses Twitch, YouTube, and Kick profile images when Streamer.bot provides them.
- Falls back to platform logos when profile images are unavailable or unsupported.
- Supports an optional platform chip on profile images.
- Supports optional profile images for Twitch, YouTube, and Kick only.
- Includes randomized preview/test mode in the dashboard.

---

## Supported Platforms and Events

### Twitch

- Follow
- Channel Point Redemption
- Bits / Cheers
- Prime Subscription
- Resubscription
- New Subscriber
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

---

## Streamer.bot Setup

1. Open Streamer.bot.
2. Go to **Servers/Clients > WebSocket Server**.
3. Enable the WebSocket server.
4. Confirm these default settings unless you intentionally changed them:
   - Address: `127.0.0.1`
   - Port: `8080`
   - Endpoint: `/`
5. Make sure each platform or integration you want alerts for is connected and receiving events inside Streamer.bot.
6. If WebSocket authentication is enforced, enter the same password in the dashboard's **General** settings before copying the OBS URL.

Recommended for most local OBS setups: keep the Streamer.bot WebSocket server local on `127.0.0.1`.

---

## GitHub Pages Setup

1. Create a GitHub repository for the alert overlay.
2. Upload these files to the repository:
   - `index.html`
   - `overlay.html`
   - `README.md`
3. Open the repository settings.
4. Go to **Pages**.
5. Set the source to the branch/folder where the files are hosted.
6. Open the published `index.html` page.

Example dashboard URL:

```text
https://USERNAME.github.io/REPOSITORY/
```

---

## Dashboard Setup

Open `index.html` in a browser.

Use the **Control Deck** to configure:

- Streamer.bot WebSocket host
- Streamer.bot WebSocket port
- WebSocket endpoint
- Optional WebSocket password
- Alert duration
- Transition time between queued alerts
- Alert position
- Alert scale
- Global sound URL
- Global volume
- Platform colors
- Platform chip visibility on profile images
- Twitch / YouTube / Kick profile image visibility
- Per-platform sound overrides
- Per-platform volume
- Event enable/disable toggles
- Event text templates

After configuration, copy the generated **OBS Browser Source URL**.

---

## OBS Setup

1. Open OBS.
2. Add a new **Browser Source**.
3. Paste the generated OBS URL from the dashboard.
4. Recommended size:
   - Width: `1920`
   - Height: `1080`
5. Enable browser source audio control if alert sounds are being used.
6. Place the browser source above gameplay/camera layers where alerts should appear.

The OBS URL contains the full configuration. The overlay does not rely on dashboard localStorage once added to OBS.

---

## Alert Queue Behavior

Alerts are displayed one at a time.

The queue uses two global timing settings:

- **Alert Duration**: how long the current alert remains visible.
- **Transition Time**: delay/animation spacing before the next queued alert appears.

If several events happen at once, they are added to the queue in the order received from Streamer.bot.

---

## Sound Behavior

Sound priority:

1. Platform sound override, if entered.
2. Global sound URL, if entered.
3. No sound.

Volume priority:

1. Platform volume setting.
2. Global volume setting.

Sound URLs should point directly to playable audio files such as `.mp3`, `.wav`, or `.ogg`.

---

## Profile Images

Profile image support is only included for:

- Twitch
- YouTube
- Kick

Other supported platforms do not include profile-image controls in the dashboard and will use the platform logo layout.

Profile images are shown only when Streamer.bot includes a usable image URL in the event payload. If the image URL is missing or fails to load, the overlay falls back to the platform logo.

---

## Event Text Templates

Each event has an editable text template.

Supported placeholders:

```text
{user}
{recipient}
{title}
{amount}
{tier}
{months}
{message}
```

Example:

```text
{user} redeemed {title} for {amount} points
```

The alert card displays `{user}` as the large headline and moves the remaining event text below it. For example, `{user} resubscribed for {months} months` displays the username as the headline and `resubscribed for 42 months` as the action line.

If a placeholder is unavailable from the event payload, the overlay will leave that value blank or use a safe fallback.

---

## Preview Mode

The dashboard preview uses the same `overlay.html` file with preview mode enabled.

Preview mode can:

- Randomly select enabled platforms.
- Randomly select enabled events.
- Use fake sample usernames, amounts, messages, and event details.
- Test individual event rows with the **Test** button.
- Clear the current preview queue.

Preview mode is intended for setup/testing only. The copied OBS URL does not include the preview flag.

---

## Troubleshooting

### Alerts are not showing in OBS

Check the following:

1. Streamer.bot is open.
2. Streamer.bot WebSocket server is enabled.
3. The dashboard WebSocket settings match Streamer.bot.
4. The platform/integration is connected in Streamer.bot.
5. The relevant platform and event are enabled in the Control Deck.
6. The OBS browser source URL was copied after making changes.

### WebSocket does not connect

Confirm:

- Host is usually `127.0.0.1`.
- Port is usually `8080`.
- Endpoint is usually `/`.
- If authentication is enforced, the password is entered in the dashboard before copying the OBS URL.

### Profile images do not show

Profile images only show for Twitch, YouTube, and Kick, and only when Streamer.bot includes a profile image URL in the event payload.

### Sounds do not play

Check:

- The audio URL points directly to an audio file.
- Browser source audio is enabled in OBS.
- The source is not muted in OBS.
- Volume is above `0` in the dashboard.

---

## Version Notes

### v0.1.1

Layout and preview revision.

Includes:

- Large username headline with smaller event action text.
- Removed platform/event tags from the alert card.
- Profile image fallback to platform logos.
- Platform logo support for non-profile-image platforms.
- Preview refresh improvements when settings change.

### v0.1.0

Initial version.

Includes:

- GitHub Pages-compatible dashboard and overlay files.
- Streamer.bot WebSocket connection.
- Direct WebSocket event subscription.
- One-at-a-time alert queue.
- General timing controls.
- Platform-specific customization sections.
- Global sound and platform sound override support.
- Preview/test mode.
- Profile image support for Twitch, YouTube, and Kick only.

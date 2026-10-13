# DropZone

**Instagram follows people. DropZone follows places.**

DropZone is a zone-based, privacy-conscious local feed for campuses, events and other shared places. People who are physically in a zone can read and post short, temporary "drops". Drops fade away unless people nearby echo them, so the feed stays useful and current instead of turning into a permanent chat.

Built for the **Samartha Hackathon** (Vignan's Institute of Information Technology), Problem Statement 05: Zone-Based Social Media.

**Live prototype:** https://likhithayeruva08-jpg.github.io/dropzone/

<!-- Add 2 or 3 screenshots here, for example:
![Zone map](screenshots/zone-map.png)
-->

## The problem

People who share a place often need quick local answers: a lost item, a question, an offer. Existing platforms are built around permanent identities, followers and broad feeds. Messages get buried, anyone can read them, and nothing expires. A place-based feed also brings its own risks: location leakage, impersonation, scams and weak moderation.

## How it works

1. **Pick a zone.** Each spot (on the VIIT campus pack: Main Block, Dharitri Block, Pharma Block, Hostel, Sagara Block, Canteen, Food Bites) has its own feed.
2. **Prove you are there.** Use your location, or scan the zone's QR code, which changes every minute.
3. **Drop it.** Post an Ask, Offer, Heads-up, Looking or Join drop. Each drop has a timer. Echoes from people in the zone add time. When time runs out, the drop expires.

## Features

- **Zone model:** circular zones (35 m radius), zone entry and exit events, and an explicit location-permission flow.
- **Venue packs:** one codebase, many venues. Switch between VIIT Campus, Railway Station, Tech Park / Event, Shopping Mall, Restaurants, Cinemas and Beaches.
- **Presence states:** inside, outside, low accuracy (worse than 50 m), spoofed, and permission denied. Each state has clear behaviour, and low-accuracy or unverified users get a read-only view.
- **Rotating zone QR:** a code that changes every minute, so a shared photo cannot be reused. Works indoors where GPS is weak, and when location is denied.
- **Drop lifecycle:** time-to-live timers, echoes (each adds half the original time, up to four), and a clear expiry status.
- **Utility modules:** lost-and-found and event Q&A through the Ask, Offer, Heads-up, Looking and Join drop types, with replies, joining and leaving a plan, claiming an offer, and marking a lost item as found.
- **Zone mood and story:** one-tap mood pulses (Crowded, Quiet, Wi-Fi slow and more), an auto summary and a zone story.
- **Official announcements:** labelled "Official" posts with a frequency cap per zone.
- **Languages:** English, Hindi and Telugu.
- **Demo tools:** a location simulator (inside, outside, low accuracy, spoofed, denied), sample activity, and a Safety tests panel.

## Safety and moderation

- Posts are screened for flagged words and scam patterns (such as UPI, OTP and short links) before they go live.
- Rate limit of 3 posts per hour per person.
- Users can report and block. Scam and privacy reports hide a drop immediately. Other reports hide it after 2 different people report it.
- A PIN-protected moderator queue lets a moderator restore or remove a drop. Removal adds a strike, and four strikes removes the identity.
- The Safety tests panel runs spoof detection, burst traffic and sample posts through the real checks.

## Privacy

- Only the zone ID is kept. Precise coordinates are not stored or shown in posts.
- Each visit gets a temporary name. The college email is turned into a scrambled ID and is used only if a drop is reported.
- Users can leave a zone or disable location at any time.
- **Honest limits:** expiry removes a drop from the live feed. It does not guarantee removal from server logs, backups or screenshots. Location checks reduce spoofing but cannot eliminate it.
- If used in schools or youth events, posting should be limited for minors and no precise location should ever be shown. (This is a policy in the privacy notice. There is no age check yet.)

## Tech stack

- HTML, CSS and vanilla JavaScript in a single file (`index.html`)
- Firebase Firestore for real-time sync across devices
- Browser Geolocation API for location
- A QR generator included in the file, with time-window tokens
- BarcodeDetector and getUserMedia for in-app camera scanning (browser dependent)
- GitHub Pages for hosting

## Run it

Open the live link above, or download `index.html` and open it in a browser. For the QR link to open on other phones, the page needs to be hosted (for example on GitHub Pages).

## Known limitations

- The in-app camera scanner needs a browser that supports QR detection. Use the phone's own camera app, paste the link, or use the demo button instead.
- The moderator PIN and QR secret are demo-only. A production version needs real staff login and server-side checks.
- Screening is rule-based, not a machine-learning model.
- There is no age verification yet.

## Roadmap

- Real authentication and server-side Firestore security rules
- Fallback QR scanner for all browsers
- Age-based restrictions for school use
- Pilot in one campus block, then venue packs for events and transit hubs
- Clearly labelled sponsored posts with frequency caps, after validating willingness to pay and moderation cost

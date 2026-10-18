# शाही विवाह निमंत्रण वेबसाइट — आर्यन एवं काव्या (डेमो)

एक-पृष्ठ (single-page) विवाह निमंत्रण वेबसाइट। कोई बिल्ड स्टेप, बैकएंड या लॉगिन नहीं — केवल एक `index.html`।

## फ़ोल्डर संरचना

```
wedding-site/
├── index.html            ← पूरी वेबसाइट (HTML + CSS + JS + CONFIG)
├── README.md
├── images/               ← (वैकल्पिक) असली फ़ोटो यहाँ रखें
│   ├── couple-hero.webp
│   ├── groom.webp
│   ├── bride.webp
│   ├── wedding-venue.webp
│   └── gallery/01.webp … 08.webp
├── videos/               ← (वैकल्पिक) love-story.mp4, prewedding-highlights.mp4, invitation-film.mp4
└── audio/                ← (वैकल्पिक) gate-chime.mp3, royal-wedding-instrumental.mp3
```

फ़ोल्डर खाली हों तब भी साइट पूरी दिखती है: हर फ़ोटो की जगह मेल खाता चित्रण (illustration) दिखता है, जिस पर “डेमो चित्रण” लिखा रहता है।

## नए ग्राहक के लिए बदलाव

`index.html` खोलें और ऊपर `const CONFIG = { … }` ढूँढें। केवल यही हिस्सा बदलें:

| क्या बदलना है | CONFIG में कहाँ |
|---|---|
| वर/वधू का नाम, उपसर्ग, माता-पिता, परिचय | `couple.groom`, `couple.bride` |
| सील पर अक्षर | `couple.groom.initial`, `couple.bride.initial` |
| परिवार का नाम (हस्ताक्षर) | `families` |
| विवाह तिथि/समय | `wedding.start`, `wedding.end` — हमेशा `+05:30` के साथ |
| दिखने वाली तिथि | `wedding.dayLabel`, `shortDate`, `timeLabel` |
| कैलेंडर कार्ड | `wedding.calendarMonth` (`firstWeekday`: 0 = रविवार) |
| स्थल | `venue.name`, `venue.city`, `venue.address`, `venue.mapsUrl`, `venue.isDemo:false` |
| कार्यक्रम | `events[]` — हर कार्यक्रम का `start`/`end` |
| फ़ोटो | `couple.heroPhoto`, `groom.photo`, `bride.photo`, `gallery[].src`, `venue.image` |
| वीडियो | `videos[].src` (MP4), `videos[].posterImg`, डेमो स्लाइड: `videos[].slides` |
| संगीत | `audio.chime`, `audio.music`, `audio.volume` |
| शायरी/आमंत्रण पाठ | `text.*` |
| रंग | `theme.*` |

**Google Maps:** वास्तविक स्थल पर Google Maps में “Share → Copy link” करें और वह लिंक `venue.mapsUrl` में डालें, फिर `isDemo:false` करें।

**फ़ोटो सुझाव:** पोर्ट्रेट 3:4 (जैसे 900×1240), हीरो 3:4 (1080×1440), गैलरी में `ratio` के अनुसार। WebP, 300 KB से कम।

## लोकल रूप से चलाना

```bash
# फ़ोल्डर में जाकर
python3 -m http.server 8080
# ब्राउज़र में खोलें: http://localhost:8080
```
(फ़ाइल पर डबल-क्लिक करके भी खुलती है, पर वीडियो/ऑडियो फ़ाइलों के लिए लोकल सर्वर बेहतर है।)

## तैनाती (Deploy)

**Netlify:** app.netlify.com → “Add new site” → “Deploy manually” → पूरा फ़ोल्डर ड्रैग-ड्रॉप करें। कुछ सेकंड में लिंक मिल जाएगा।

**Vercel:** vercel.com → “Add New Project” → GitHub रिपॉज़िटरी चुनें (या `npx vercel` कमांड) → Framework: “Other” → Deploy।

तैनाती के बाद `index.html` के `<head>` में `og:image` के लिए पूरा URL जोड़ें (1200×630 का चित्र), ताकि WhatsApp पर सुंदर प्रीव्यू दिखे।

## संपत्ति (Assets) चेकलिस्ट — अभी देना बाकी

- [ ] वर-वधू की हीरो फ़ोटो (`couple-hero.webp`)
- [ ] वर का पोर्ट्रेट (`groom.webp`), वधू का पोर्ट्रेट (`bride.webp`)
- [ ] 6–8 प्री-वेडिंग फ़ोटो (`gallery/`)
- [ ] स्थल की फ़ोटो (`wedding-venue.webp`) + सत्यापित Maps लिंक + पूरा पता
- [ ] 3 वीडियो MP4 (H.264, 720p/1080p, 10 MB से कम) + पोस्टर इमेज
- [ ] लाइसेंसशुदा वाद्य संगीत (शहनाई/बाँसुरी/सितार) — कॉपीराइट वाले फ़िल्मी गाने नहीं
- [ ] (वैकल्पिक) लाइसेंसशुदा गणेश जी का चित्र
- [ ] og:image प्रीव्यू चित्र (1200×630)

## ईमानदार नोट

- “हमारी प्रेम कहानी” में तीन छोटी डेमो फ़िल्में चलती हैं, जो चित्रों से बनी स्लाइड-फ़िल्म हैं (zoom + text + संगीत)। `videos[].src` में MP4 डालते ही उसी जगह असली वीडियो चलेगा। स्लाइड का क्रम/पाठ `videos[].slides` में बदलें।
- संगीत अभी ब्राउज़र में Web Audio से बनाई गई डेमो धुन है (तानपुरा + बाँसुरी जैसी ध्वनि, भूपाली राग के स्वर)। असली रिकॉर्डिंग `audio.music` में डालें।
- चित्र SVG चित्रण हैं, असली फ़ोटो नहीं — हर जगह “डेमो” लेबल है।
- “शुभ तिथि सहेजें” बटन Google Calendar का पहले से भरा कार्यक्रम खोलता है (IST समय)।
- कोई RSVP, WhatsApp बटन या संपर्क फ़ॉर्म नहीं है।

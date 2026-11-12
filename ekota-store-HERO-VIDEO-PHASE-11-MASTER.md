# ekota.store — হিরো ভিডিও ও প্রচার-সামগ্রী: সম্পূর্ণ ফাইল (Phase 11)

> এই ফাইলে আছে: (A) উদ্দেশ্য ও ফিচার, (B) যে সিদ্ধান্তগুলো আমি আপনার হয়ে নিয়েছি, (C) চূড়ান্ত ভিডিও স্ক্রিপ্ট (মিউজিকহীন), (D) ভিডিও বানানোর ব্রিফ, (E) AI এজেন্টের জন্য Phase 11 নির্দেশনা, (F) আপনার জন্য কনটেন্ট আপডেটের নিয়ম, (G) প্রকাশের আগের চেকলিস্ট।
> **ব্যবহারের নিয়ম:** মূল প্রজেক্ট (Phase 1–10) শেষ হওয়ার পর এই ফাইলটি `docs/PHASE_11_HERO_VIDEO.md` নামে রিপোতে রাখুন এবং এজেন্টকে বলুন: "Execute Phase 11 per CLAUDE.md + docs/PHASE_11_HERO_VIDEO.md Part E."
> **নোট:** এই ফাইল `CLAUDE.md`-এর কোনো Locked Decision বদলায় না। নতুন সিদ্ধান্তের প্রস্তাব Part B-তে আছে, আপনি নিজে `docs/DECISIONS.md`-এ যোগ করবেন।

---

# PART A — উদ্দেশ্য ও ফিচার

## উদ্দেশ্য
১. সাইটে যিনিই আসেন, হিরো সেকশনের ভিডিও দেখে ৫ মিনিটে ekota.store কী করে, কীভাবে করে, আর কী করে না, বুঝে নিতে পারবেন।
২. প্রচারকারী (Promoter) ও পার্টনারদের হাতে তৈরি প্রচার-সামগ্রী তুলে দেওয়া, যাতে তাঁদের কাজ সহজ হয় এবং সবাই একই সঠিক বার্তা ছড়ান।
৩. ভুল ধারণা কমানো: ekota.store ডেলিভারি দেয় না, টাকা ধরে না, আয়ের নিশ্চয়তাও দেয় না।
৪. ভিডিও বা সামগ্রী আপডেট বা নতুন ভাষা যোগ করার কাজ আপনি কোডে হাত না দিয়েই করতে পারবেন।

## ফিচার তালিকা
| # | ফিচার | কে ব্যবহার করবেন | মূল কথা |
|---|---|---|---|
| ১ | হিরো ভিডিও | সবাই | পোস্টার + প্লে বোতাম, ট্যাপ করলে ভিডিও লোড। নিজে নিজে চালু হবে না। |
| ২ | ভাষা বদল | সবাই | ভিডিও, পোস্টার, সাবটাইটেল ভাষা অনুযায়ী। নতুন ভাষা যোগ হবে ফাইল রেখে। |
| ৩ | সাবটাইটেল | সবাই | একাধিক ভাষার সাবটাইটেল বেছে নেওয়া যাবে। |
| ৪ | রিঅ্যাকশন | লগইন করা ব্যবহারকারী | লাইক, ভালোবাসা, অনুপ্রাণিত। এক ব্যবহারকারী এক রিঅ্যাকশন। |
| ৫ | কমেন্ট | লগইন করা ব্যবহারকারী | সীমা, রিপোর্ট, অটো-হাইড। |
| ৬ | শেয়ার | সবাই | ফোনের শেয়ার মেনু, WhatsApp, লিঙ্ক কপি। |
| ৭ | ভিডিও পেজ (`/watch`) | সবাই | সরাসরি লিঙ্কে খোলে, শেয়ারে সুন্দর প্রিভিউ আসে। |
| ৮ | প্রচার-সামগ্রী লাইব্রেরি | যাচাইকৃত Promoter ও Partner | ভিডিও, পোস্টার, ছবি, ব্যানার, ক্যাপশন, গাইড ডাউনলোড। |
| ৯ | আমার প্রচার-কিট | যাচাইকৃত Promoter ও Partner | নিজের প্রমো লিঙ্ক, QR কোড, কপি করার মতো ক্যাপশন। |
| ১০ | কনটেন্ট আপডেট | শুধু আপনি | স্টোরেজে ফাইল বদলান + ছোট একটি ম্যানিফেস্ট ফাইল সম্পাদনা। আলাদা অ্যাডমিন প্যানেল নেই। |

---

# PART B — আমার নেওয়া সিদ্ধান্ত (পছন্দ না হলে বলবেন)

| বিষয় | সিদ্ধান্ত | কারণ |
|---|---|---|
| ভিডিও কোথায় থাকবে | নিজের S3-সামঞ্জস্যপূর্ণ স্টোরেজে (R2/Supabase), যা প্রজেক্টে আগে থেকেই আছে | সস্তা, নিয়ন্ত্রণ আপনার হাতে, ফাইল বদলালেই আপডেট। |
| আপডেটের পদ্ধতি | একই নামের ফাইল রিপ্লেস + `manifest.json`-এর `version` সংখ্যা বাড়ানো | আলাদা অ্যাডমিন প্যানেল লাগে না। |
| কমেন্ট | সঙ্গে সঙ্গে দেখা যাবে, কিন্তু রিপোর্ট হলে (ডিফল্ট ৩টি) নিজে লুকিয়ে যাবে | নতুন অনুমোদনের প্যানেল না বানিয়ে চালানোর সহজ উপায়। |
| কমেন্ট মডারেশন | Phase 10-এর বিদ্যমান অ্যাডমিন মডারেশন তালিকায় একটি নতুন ধরন ("হিরো কমেন্ট") যোগ হবে | এটাই একমাত্র অ্যাডমিন-পরিবর্তন, আর তা জরুরি। কমেন্ট লুকানোর উপায় না থাকলে ঝুঁকি। |
| কমেন্ট বন্ধ রাখার উপায় | `AppConfig.heroVideoCommentsEnabled = false` | মডারেশন প্রস্তুত না থাকলে বন্ধ রাখা যায়। |
| ভিডিওতে টাকার অঙ্ক | ভিডিওতে নির্দিষ্ট ডলার/শতাংশ বলা হবে না, "সাশ্রয়ী বার্ষিক ফি", "বিশেষ ছাড়", "কমিশন" বলা হবে। সঠিক অঙ্ক সাইটে দেখানো হবে। | অঙ্ক বদলালে ভিডিও পুরোনো হয়ে যাবে। প্রতিটি ভাষার ভিডিও আবার বানানো ব্যয়বহুল। |
| শব্দ | কোনো মিউজিক নেই। শুধু ভয়েসওভার, প্রাকৃতিক শব্দ আর সংক্ষিপ্ত UI সাউন্ড (নোটিফিকেশন, ট্যাপ)। | আপনার নির্দেশনা। |
| ডাউনলোডের অধিকার | শুধু যাচাইকৃত (KYC VERIFIED) Promoter ও Partner | ভুয়া প্রচারকারী বা অযাচাইকৃত কেউ যেন ব্যবহার না করে। |

## DECISIONS.md-এর জন্য প্রস্তাবিত এন্ট্রি (আপনি নিজে যোগ করবেন)
- **D23:** Phase 11 (Hero Video + Promoter/Partner Ad Materials) is approved. It changes no Locked Decision 1-22.
- **D24:** Hero video and ad materials are updated by replacing files in object storage and bumping `version` in the manifest. No dedicated admin panel. Comment moderation reuses the Phase 10 admin moderation queue.
- **D25:** The hero video contains NO music. Only voiceover, natural ambient sound, and short UI sound effects.
- **D26:** Video narration does not state specific prices, percentages, or commission rates.

---

# PART C — চূড়ান্ত ভিডিও স্ক্রিপ্ট (মিউজিকহীন)

**শিরোনাম:** ekota.store — মাটির টান, সম্ভাবনার পথ
**দৈর্ঘ্য:** আনুমানিক ৫ মিনিট
**ভাষা:** বাংলা ভয়েসওভার + ইংরেজি সাবটাইটেল
**স্থান:** কোনো নির্দিষ্ট এলাকার নাম নেই
**ফেসলেস:** কোনো মুখ দেখানো হবে না

## শব্দ-নীতি (কঠোরভাবে মানতে হবে)
- **অনুমোদিত:** ভয়েসওভার, প্রাকৃতিক শব্দ (পাখি, বৃষ্টি, বাতাস, পানি, পাতার শব্দ, দূরের গরুর ডাক, সাইকেলের চাকা ও ঘণ্টি, পায়ের শব্দ), সংক্ষিপ্ত UI সাউন্ড (নোটিফিকেশনের "পিং", স্ক্রিন ট্যাপ)।
- **নিষিদ্ধ:** যেকোনো ধরনের সুর, বাদ্যযন্ত্র, গুনগুন, ছন্দময় বিট, নাশিদ বা গান। আজান বা ধর্মীয় আবৃত্তি ব্যাকগ্রাউন্ড শব্দ হিসেবে নয়।
- **UI সাউন্ড:** ছোট, একক ও সুরহীন টোন। কোনো মেলোডিক নোটিফিকেশন নয়।
- **স্টক ফুটেজ:** কেনা বা ডাউনলোড করা ক্লিপের নিজস্ব অডিও সরিয়ে ফেলে শুধু নিজের তৈরি প্রাকৃতিক শব্দ বসাবেন, যাতে কোনো লুকানো মিউজিক না থাকে।
- **আবেগ আনার উপায়:** মিউজিক ছাড়া আবেগ আসবে ভয়েসের ধীর গতি, নীরবতার বিরতি আর প্রকৃতির শব্দের ওঠানামায় (যেমন বৃষ্টি বাড়ে, বাতাস নরম হয়, পাখির ডাক ধীরে ফোটে)।

## দৃশ্য ১: গ্রামের ভোর (০:00–০:35)
**ভিজ্যুয়াল:** পূর্ব আকাশে সোনালি আলো। ধানক্ষেতের ওপর হালকা কুয়াশা, পাতার ডগায় শিশির। পুকুরে শাপলা, দূরে বাঁশঝাড়, নদীর ঘাটে নৌকা। টিনের চালে ভোরের আলো। রান্নাঘরে একজোড়া হাত চুলায় আগুন ধরাচ্ছে। হাত একটা খালি কৌটার ঢাকনা তুলে দেখে, আস্তে বন্ধ করে।
**সাউন্ডস্কেপ:** পাখির কিচিরমিচির ধীরে বাড়ছে, হালকা বাতাস, ধানের পাতার মৃদু সরসর, কাঠের চুলায় আগুনের ফট ফট, ঢাকনা বন্ধের ছোট শব্দ।

**ভয়েসওভার:**
> "এই গ্রামে ভোর আসে ধীরে। শিশির ভেজা ধানের ডগায়, পুকুরের শাপলায়, আর টিনের চালে সোনালি আলো হয়ে।
> এখানে সবকিছু আছে, শুধু সব সময় হাতের কাছে নেই।
> রান্নাঘরে মা কৌটা খুলে দেখলেন, শুকনা ঝাল শেষ। হাট বসবে আরও দুদিন পর।"

## দৃশ্য ২: প্রবাসের রাত, মায়ের কথা (০:35–১:10)
**ভিজ্যুয়াল:** দূর প্রবাসের এক রাত। উঁচু ভবনের জানালা, বাইরে বৃষ্টি, নিচে আলো ঝলমলে শহর। একজোড়া হাত ফোন তুলে কল করছে, স্ক্রিনে শুধু "মা"। কাঁধের ওপর দিয়ে দেখা যায় হাতে একটি বাঁধানো পারিবারিক ছবি, মুখ আলো-ছায়ায় অস্পষ্ট।
**সাউন্ডস্কেপ:** জানালার কাচে বৃষ্টির ফোঁটা, দূরের শহরের মৃদু গুঞ্জন, কলের রিং-টোন (সংক্ষিপ্ত, সুরহীন), ফোনের ওপাশের কণ্ঠ।
**অন-স্ক্রিন টেক্সট:** *Far from home.*

**মায়ের কণ্ঠ (শুধু অডিও):** "কিছু লাগবে না রে বাবা। তুই খেয়েছিস?"

**ভয়েসওভার:**
> "মায়েরা এভাবেই বলেন। 'কিছু লাগবে না।'
> হাজার হাজার মাইল দূরে বসে শামীম জানেন, সত্যিটা কখনো কখনো এর উল্টো।
> তিনি চান মায়ের পাশে দাঁড়াতে, কিন্তু মাঝখানে পড়ে আছে সমুদ্র, আকাশ আর ঘুম না আসা রাত।"

## দৃশ্য ৩: তিনটি বিচ্ছিন্ন বিন্দু (১:10–১:40)
**ভিজ্যুয়াল:** গোধূলির আলো। গ্রামের মুদি দোকান, তাকে সাজানো জিনিস, দাঁড়িপাল্লা, একজোড়া হাত খাতায় হিসাব লিখছে, সামনে কেউ নেই। মেঠো পথের পাশে এক তরুণ, পেছন থেকে, সাইকেল ধরে দিগন্তের দিকে তাকিয়ে। ছোট অফিসের জানালায় ল্যাপটপের আলোয় এক ছায়া। ২ডি অ্যানিমেশনে তিনটি আলাদা আলোর বিন্দু, মাঝে অন্ধকার।
**সাউন্ডস্কেপ:** কলম চলার খসখস, দাঁড়িপাল্লার ক্ষীণ ধাতব শব্দ, দূরে গরুর ফেরার ডাক, বাতাস, ঝিঁঝি পোকা ধীরে ফুটছে।

**ভয়েসওভার:**
> "গ্রামের মুদি দোকানি শাওন। সবাই চেনে তাঁকে, তবু দোকান ফাঁকা পড়ে থাকে।
> সাইকেল হাতে এক তরুণ, যার সময় আছে, শক্তি আছে, শুধু কাজটা নেই।
> আর এক উদ্যমী যুবক, যিনি জানেন, ছোট দোকানগুলো একটু সাহায্য পেলেই অনেক দূর যেতে পারে।
> তিনজনেরই স্বপ্ন আছে। শুধু একে অপরকে খুঁজে পাওয়ার পথটা নেই।"

## দৃশ্য ৪: সেতু (১:40–২:00)
**ভিজ্যুয়াল:** তিনটি আলোর বিন্দুর মাঝে সোনালি রেখা টান পড়ে, রেখাগুলো মাঠ, নদী, রাস্তা পেরিয়ে ছড়ায়। লোগো **ekota.store**। নিচে ট্যাগলাইন: *Connecting Markets, Empowering Lives.*
**সাউন্ডস্কেপ:** ঝিঁঝি থেমে যায়, এক মুহূর্ত নীরবতা, তারপর সকালের পাখির ডাক আবার ধীরে ফিরে আসে। রেখা জোড়ার সময় একটি সংক্ষিপ্ত, সুরহীন "ক্লিক"।

**ভয়েসওভার:**
> "সেই পথটাই ekota.store। 'ঐক্য' মানে একসাথে।
> এখানে দোকানি, তরুণ, উদ্যোক্তা আর প্রবাসে থাকা সন্তান, সবাই এক সুতোয় বাঁধা পড়েন।"

## দৃশ্য ৫: কীভাবে কাজ করে (২:00–২:35)
**ভিজ্যুয়াল:** পরিষ্কার মোশন-গ্রাফিক্স, তিন ধাপ পরপর:
১. *খুঁজুন* (মানচিত্রে কাছের দোকান)
২. *কথা বলুন* (WhatsApp-এ সরাসরি)
৩. *নিজেরা মিটিয়ে নিন* (লেনদেন ক্রেতা-বিক্রেতার মধ্যে)
পাশে তিনটি ব্যাজ: *ID Verified · Face Verified · Direct WhatsApp* (মুখ-যাচাই শুধু আইকনে)।
**সাউন্ডস্কেপ:** পরিষ্কার, শান্ত পরিবেশ। প্রতিটি ধাপ আসার সময় একটি করে হালকা, সুরহীন ট্যাপ।

**ভয়েসওভার:**
> "ekota.store কোনো সাধারণ অনলাইন দোকান নয়।
> আমরা পণ্য বিক্রি করি না, ডেলিভারি দিই না, আপনাদের লেনদেনের টাকাও ধরি না।
> আমরা শুধু একজনকে আরেকজনের কাছে পৌঁছে দিই। কথা, দরদাম আর ডেলিভারির ব্যবস্থা, ক্রেতা আর বিক্রেতা WhatsApp-এ সরাসরি ঠিক করে নেন।
> আর বিশ্বাসের জন্য প্রতিটি বিক্রেতা ও সেবাদাতার পরিচয়পত্র ও মুখ যাচাই করা হয়।"

## দৃশ্য ৬: বিক্রেতা, বৃষ্টির দিনে প্রথম বার্তা (২:35–৩:05)
**ভিজ্যুয়াল:** ঝমঝম বর্ষা। টিনের চালে বৃষ্টি, উঠোনে জমা জল। একটি হাত ফোনে পণ্যের ছবি তুলছে। বাংলায় স্টোরের পাতা তৈরি হচ্ছে। দোকানের দেয়ালে QR কোডসহ পোস্টার। হঠাৎ স্ক্রিনে বার্তা: "ভাই, শুকনা ঝাল আছে?" হাতটা থমকে যায়, তারপর টাইপ করে।
**সাউন্ডস্কেপ:** টিনের চালে বৃষ্টির তীব্র শব্দ, একটি ছোট নোটিফিকেশন "পিং" আসতেই বৃষ্টি নরম হয়, টাইপের মৃদু টকটক।

**ভয়েসওভার:**
> "বর্ষার এক দুপুরে শাওন প্রথমবার নিজের দোকানের নাম একটা ফোনের পর্দায় দেখলেন।
> বাংলায়, নিজের ভাষায়, নিজের ফোনেই, দোকান সাজালেন তিনি। সঙ্গে পেলেন একটা মার্কেটিং কিট: নিজস্ব QR কোড দেওয়া পোস্টার আর ভিজিটিং কার্ড।
> আর কিছুক্ষণ পরে এল সেই প্রথম বার্তা, 'ভাই, আছে?'
> এর জন্য শুধু একটি সাশ্রয়ী বার্ষিক ফি।"

**অন-স্ক্রিন টেক্সট:** *Simple yearly plans. See current plans on the website.*

## দৃশ্য ৭: পার্টনার ও প্রমোটার, হাত ধরে এগিয়ে দেওয়া (৩:05–৩:40)
**ভিজ্যুয়াল:** সোনালি বিকেল। ছোট অফিসের টেবিলে ল্যাপটপ, চায়ের কাপ। একের পর এক দোকানের স্টোর তৈরি হচ্ছে, প্রতিটির পাশে সবুজ টিক। হিসাবের স্ক্রিনে "বিশেষ ছাড়" হাইলাইট। কাট করে একজন ডিজিটাল ক্রিয়েটরের মোবাইল এডিটিং স্ক্রিন, তাতে একটি প্রমো কোড।
**সাউন্ডস্কেপ:** কিবোর্ডের টাইপিং, চায়ের কাপ নামানোর ক্ষীণ শব্দ, বাইরে বিকেলের পাখি, প্রতিটি টিক এলে ছোট সুরহীন "ক্লিক"।

**ভয়েসওভার:**
> "যাঁরা প্রযুক্তি জানেন, তাঁরা পাশের দোকানদারের হাত ধরতে পারেন।
> পার্টনার সামান্য বার্ষিক ফিতে যোগ দিয়ে দোকানদারদের স্টোর সেটআপ করে দেন, আর এই কাজে পান বিশেষ ছাড়। সেই ছাড় তাঁর নিজের উপার্জন।
> আর যাঁরা ডিজিটাল ক্রিয়েটর, তাঁরা নিজের প্রমো কোড বানান। সেই কোডে কেউ স্টোর খুললে তিনি কমিশন পান।
> এভাবেই একজন এগোলে আরও কয়েকজন এগিয়ে যান।"

**অন-স্ক্রিন টেক্সট (ছোট হরফে):** *Commission is confirmed after a holding period and paid monthly. Earnings depend on your effort.*

## দৃশ্য ৮: সেবাদাতা, সাইকেলের পথে (৩:40–৪:05)
**ভিজ্যুয়াল:** সূর্যাস্ত। ধানক্ষেতের আল ধরে সাইকেলের চাকা ঘুরছে। পেছন থেকে এক তরুণ, কাঁধে ব্যাগ। দূরে গরুর পাল ফিরছে, আকাশ কমলা। ফোনের স্ক্রিনে তাঁর প্রোফাইল: "বাজার করে দেওয়া, হোম ডেলিভারি", সবুজ "Verified" ব্যাজ, রেটিং, দূরত্ব। এরপর মেকানিক ও ইলেকট্রিশিয়ানের প্রোফাইল।
**সাউন্ডস্কেপ:** সাইকেলের চাকার ঘুরঘুর, মাঝে মাঝে ঘণ্টির টুংটাং, ঘাসে বাতাসের শব্দ, গোধূলির পাখি।

**ভয়েসওভার:**
> "আর আছেন সেবাদাতা।
> যাঁর সাইকেল আছে, দক্ষতা আছে, কিংবা শুধু কাজ করার মন আছে, তিনিও নিজের সেবার তালিকা দিতে পারেন: বাজার করে দেওয়া, ডেলিভারি, মেরামত, ইলেকট্রিক কাজ।
> দোকানদার বা ক্রেতা দূরত্ব, রেটিং আর যাচাইয়ের ব্যাজ দেখে ঠিক মানুষটিকে বেছে নেন।
> একটা সাইকেলই হয়ে উঠতে পারে একটা নতুন শুরুর নাম।"

## দৃশ্য ৯: সেই রাতের সমাপ্তি (৪:05–৪:40)
**ভিজ্যুয়াল:** আবার প্রবাসের রাত। হাতে ফোন, সার্চ বক্সে "শুকনা ঝাল"। রেডিয়াস ১০ কিমি, "লোকাল" নির্বাচিত। মানচিত্রে মায়ের গ্রামের আশপাশের দোকান পিন হচ্ছে। শাওনের দোকানের কার্ডে দাম, দূরত্ব, "আনুমানিক ডেলিভারি সময়"। WhatsApp বোতামে আঙুল। শাওনের ফোনে বার্তা, তারপর মেঠো পথে সাইকেলের চাকা। গ্রামের উঠোন, মাটির দাওয়া, একজোড়া হাত কৌটাটা নিচ্ছে, ঢাকনা খুলে গন্ধ নিচ্ছে। ফোনে মায়ের ভিডিও কল, শামীমের হাত স্ক্রিন ছুঁয়ে।
**সাউন্ডস্কেপ:** প্রবাসের বৃষ্টি নরম হয়ে আসে, ট্যাপের শব্দ, নোটিফিকেশন "পিং", সাইকেলের ঘণ্টি, উঠোনে পায়ের শব্দ, ঢাকনা খোলার শব্দ, দূরে পাখির ডাক। শেষ মুহূর্তে মায়ের কণ্ঠ আর নীরবতা।

**মায়ের কণ্ঠ (শুধু অডিও):** "কে পাঠাল রে এত তাড়াতাড়ি?"

**ভয়েসওভার:**
> "শামীম ekota.store খুললেন। লিখলেন, 'শুকনা ঝাল'। গ্রামের দশ কিলোমিটারের মধ্যে, লোকাল দোকান।
> সামনে এল মায়ের গ্রামের দোকানগুলো, কার কত দাম, কত দূরে, আনুমানিক কত সময়ে পৌঁছাবে।
> এক ক্লিকে শাওনের সাথে কথা। পৌঁছে দেওয়ার ভার নিল সেই সাইকেলের তরুণ।
> কিছুক্ষণ পর, হাজার মাইল দূরের উঠোনে, মা কৌটাটা নিলেন।
> আর ওপাশ থেকে ভেসে এল সেই কণ্ঠ, 'কে পাঠাল রে এত তাড়াতাড়ি?'"

**অন-স্ক্রিন টেক্সট:** *Delivery times are estimates. Details are agreed directly on WhatsApp.*

## দৃশ্য ১০: সম্ভাবনার দিগন্ত (৪:40–৫:00)
**ভিজ্যুয়াল:** ধীর, কোমল মন্টাজ। সূর্যোদয়ের আলোয়: দোকানের তাকে ধীরে আরও পণ্য সাজানো হচ্ছে (হাত); সাইকেলের পাশে আরেকটি সাইকেল, দুজনের ছায়া; এক গৃহিণীর হাত আচারের বয়াম সাজাচ্ছে, লেবেলে বাংলা লেখা; এক ছাত্রের হাত বই খুলছে, টেবিলে ফোন; সোনালি ধানের মাঠ। গ্রামের আলোগুলো নেটওয়ার্কের বিন্দু হয়ে পুরো দেশ ছাড়িয়ে ছড়ায়। কালো স্ক্রিনে লোগো ও ডোমেইন।
**সাউন্ডস্কেপ:** সকালের পাখির ডাক পূর্ণ হয়, বাতাসে ধানের শীষের নড়াচড়া, শেষে ধীরে সব শব্দ মিলিয়ে গিয়ে এক মুহূর্তের নীরবতা।

**ভয়েসওভার:**
> "একটা দোকান, একটা সাইকেল, একটা ফোন। ছোট শুরু। কিন্তু প্রতিটি বড় পথচলাই শুরু হয় ছোট এক পদক্ষেপে।
> আপনার গ্রাম, আপনার পাড়া, আপনার হাতের কাজ, এগুলো ছোট নয়। এগুলোই সম্ভাবনার বীজ।
> কোনো জটিল পেমেন্ট নয়, কোনো গুদামের ঝামেলা নয়। শুধু মানুষের সাথে মানুষের সংযোগ।
> আজ আপনার এলাকা, কাল আপনার পুরো দেশ।
> ekota.store। Connecting Markets, Empowering Lives।"

**অন-স্ক্রিন টেক্সট:** **ekota.store**
**ছোট হরফে:** *Opportunity, not a promise. Your effort makes it grow.*

## ভুল ধারণা এড়ানোর নিয়ম
| ভুল ধারণা | সঠিক বার্তা |
|---|---|
| ekota.store ডেলিভারি দেয় | ডেলিভারি দেন বিক্রেতা বা তাঁর বেছে নেওয়া সেবাদাতা। |
| অ্যাপে টাকা দেওয়া যায় / ekota.store টাকা ধরে | লেনদেন ক্রেতা-বিক্রেতার সরাসরি। |
| ekota.store নিজে পণ্য বিক্রি করে | বিক্রি করেন বিক্রেতারা। |
| যোগ দিলেই নিশ্চিত আয় | "সম্ভাবনা" বলুন, "নিশ্চয়তা" নয়। |
| ডেলিভারির সময় নিশ্চিত | সবসময় "আনুমানিক"। |
| ইন্টারন্যাশনাল বিক্রয় এখনই চালু | প্রথম সংস্করণে দেশের মধ্যে। ভিডিওতে চালু বলা যাবে না। |
| প্রমোটারের কমিশন সাথে সাথে ব্যাংকে | কিছুদিনের হোল্ডের পর অনুমোদন, মাসিক পেআউট। |
| যাচাই ছাড়াই বিক্রেতা হওয়া যায় | পরিচয়পত্র/পাসপোর্ট ও মুখ যাচাই বাধ্যতামূলক। |
| ডাক্তার/চিকিৎসা-সেবা স্বয়ংক্রিয়ভাবে প্রকাশ হয় | চিকিৎসা-সংক্রান্ত তালিকা অনুমোদনসাপেক্ষ। ভিডিওতে ডাক্তারের উল্লেখ নেই। |

## ভাষা যোগের জন্য অনুবাদ-নির্দেশ
- প্রতিটি দৃশ্যের নম্বর (১–১০) ঠিক রেখে অনুবাদ করুন। ভয়েসওভারের বাক্যের ক্রম ও বিরতি অপরিবর্তিত থাকবে।
- নতুন ভাষার জন্য লাগবে: নতুন ভয়েসওভার, সেই ভাষার সাবটাইটেল (VTT) ও পোস্টার। ভিজ্যুয়াল ও সাউন্ডস্কেপ একই থাকবে, শুধু ভয়েস ট্র্যাক বদলাবে। তাই শেষ এডিটে ভয়েস, প্রাকৃতিক শব্দ ও UI সাউন্ড আলাদা ট্র্যাকে রাখবেন।
- ভিডিওর স্ক্রিন-টেক্সট ওভারলেও আলাদা ট্র্যাকে রাখুন, যাতে অনুবাদে সহজে বদলানো যায়।

---

# PART D — ভিডিও বানানোর ব্রিফ (মানুষ বা ভিডিও-টুলের জন্য)

> **গুরুত্বপূর্ণ:** কোডিং এজেন্ট ভিডিও বানাবে না। ভিডিও আলাদাভাবে তৈরি হবে। তৈরি ভিডিও আপলোড করলে এজেন্টের বানানো সিস্টেম সেটা দেখাবে।

## ডেলিভারেবল
| ফাইল | বিবরণ |
|---|---|
| মাস্টার ভিডিও | ১৬:৯, ১০৮০p, প্রায় ৫ মিনিট |
| `video-480.mp4` | ডিফল্ট ও কম ডেটার জন্য |
| `video-720.mp4` | ভালো মানের জন্য |
| `poster.jpg` | ১২৮০×৭২০, ১৫০ KB-এর মধ্যে, ভিডিওর সবচেয়ে সুন্দর ফ্রেম (মুখ ছাড়া) |
| `captions-bn.vtt`, `captions-en.vtt` | UTF-8, ভয়েসওভারের সঠিক সময় অনুযায়ী |
| ছবির সেট | পোস্টার, ব্যানার, স্টোরি (৯:১৬), সোশ্যাল (১:১), লোগো |
| ছোট ক্লিপ | ৬০ সেকেন্ড ও ৩০ সেকেন্ডের সংস্করণ, ৯:১৬ |

## এনকোডিং (ffmpeg)
```bash
# 480p: ডিফল্ট
ffmpeg -i master.mp4 -vf scale=-2:480 -c:v libx264 -crf 28 -preset slow \
  -c:a aac -b:a 96k -movflags +faststart video-480.mp4

# 720p
ffmpeg -i master.mp4 -vf scale=-2:720 -c:v libx264 -crf 26 -preset slow \
  -c:a aac -b:a 128k -movflags +faststart video-720.mp4
```
`+faststart` ছাড়া ভিডিও সম্পূর্ণ ডাউনলোড না হওয়া পর্যন্ত চলবে না, তাই ভুলবেন না।

## শুটিং/ফুটেজ নির্দেশনা
- **ফেসলেস:** হাত, পেছন থেকে অবয়ব, ছায়া, অ্যানিমেশন, প্রকৃতি। কোনো আসল মানুষের মুখ বা স্টক ফটো নয়।
- **স্থান-নিরপেক্ষ:** ফ্রেমে কোনো সাইনবোর্ড, ল্যান্ডমার্ক বা চেনা স্থানের চিহ্ন রাখবেন না।
- **প্রকৃতির দৃশ্য:** ভোরের কুয়াশা, শিশির, শাপলার পুকুর, বাঁশঝাড়, নদীর ঘাট, বর্ষা, গোধূলির গরুর পাল, সোনালি ধানক্ষেত।
- **লাইসেন্স:** শুধু বাণিজ্যিক ব্যবহারের অনুমতিসহ বা রয়্যালটি-ফ্রি ফুটেজ। লাইসেন্সের প্রমাণ `docs/licenses/` ফোল্ডারে রাখুন।
- **UI স্ক্রিন:** আসল সাইটের চূড়ান্ত ডিজাইন থেকে রেকর্ড করুন, কাল্পনিক ডিজাইন নয়। ডেমো ডেটা ভিডিওর জন্য আলাদা, প্রোডাক্টের সিড ডেটার অংশ নয়।

## শব্দ-ডিজাইন
- ট্র্যাক আলাদা রাখুন: (১) ভয়েসওভার, (২) প্রাকৃতিক শব্দ, (৩) UI সাউন্ড, (৪) মায়ের কণ্ঠ।
- শেষ মিক্সে কোনো সুর বা বাদ্যযন্ত্র নেই কি না, **একজন মানুষ পুরো ভিডিও হেডফোনে শুনে** নিশ্চিত করবেন।

---

# PART E — AI এজেন্টের নির্দেশনা: PHASE 11 (English, for the coding agent)

> Read CLAUDE.md in full first (precedence rule at the top applies). Then read docs/DECISIONS.md and docs/PHASE_STATE.md. This part adds Phase 11 only. It must not change Locked Decisions 1-22.

## E.0 Preconditions
- Phases 1-10 are DONE in PHASE_STATE (need: auth, KYC states, Partner/Promoter roles and PromoCode, QR lib, Phase 10 admin moderation).
- If a precondition is missing: write `BLOCKED-ON-HUMAN` / `BLOCKED-ON-PHASE` in PHASE_STATE and stop. Do not stub around it.
- **You do NOT produce the video.** Build the player, manifests, reactions, comments, share, and the materials library. The owner uploads the actual files. Until they exist the hero must render gracefully WITHOUT a video (no errors, no empty box).

## E.1 Scope (Phase 11 only)
In scope: hero video section, `/[locale]/watch` page, reactions, comments (with moderation hook), share, promoter/partner materials library, personal promo kit.
Out of scope: dedicated admin panel/CMS, video transcoding pipeline, HLS/DASH, video upload UI, in-app recording, anything touching pricing/commission math, Phase 12+ ideas. If a new decision is needed, STOP and ask ONE question.

## E.2 Sub-steps (checkpoint after each: tests → commit → PHASE_STATE)
| Step | Content |
|---|---|
| 11.1 | Manifest loader + Zod schemas + public URL builder + hero poster/player (lazy) + language/quality/caption selection + graceful fallback |
| 11.2 | Reactions + comments + report/auto-hide + moderation-queue hook + share menu + `/watch` page + SEO |
| 11.3 | Materials library (private bucket, signed downloads) + personal promo kit + audit + rate limits |
| 11.4 | i18n strings, accessibility pass, performance verification on Netlify, docs for owner, Self-Test |

## E.3 Storage layout & manifests (NO admin panel)
Owner updates content by replacing files in storage and editing a small manifest. Use the existing S3-compatible storage (`S3_ENDPOINT`, `S3_BUCKET_PUBLIC`, `S3_BUCKET_PRIVATE`).

**Public bucket (hero, streamed to everyone):**
```
hero/manifest.json
hero/<lang>/video-480.mp4
hero/<lang>/video-720.mp4
hero/<lang>/poster.jpg
hero/<lang>/captions-<lang>.vtt
```
**Private bucket (materials, downloads only for verified Promoter/Partner):**
```
materials/manifest.json
materials/<category>/<file>
```

`hero/manifest.json` example:
```json
{
  "version": 1,
  "videoKey": "hero-explainer",
  "defaultLanguage": "bn",
  "variants": [
    {
      "language": "bn",
      "title": "ekota.store — মাটির টান, সম্ভাবনার পথ",
      "durationSec": 300,
      "poster": "hero/bn/poster.jpg",
      "sources": [
        { "height": 480, "src": "hero/bn/video-480.mp4" },
        { "height": 720, "src": "hero/bn/video-720.mp4" }
      ],
      "captions": [
        { "language": "bn", "label": "বাংলা", "src": "hero/bn/captions-bn.vtt" },
        { "language": "en", "label": "English", "src": "hero/bn/captions-en.vtt" }
      ]
    }
  ]
}
```

`materials/manifest.json` example:
```json
{
  "version": 1,
  "items": [
    {
      "id": "poster-a4-bn",
      "category": "POSTER",
      "type": "FILE",
      "titleBn": "পোস্টার (A4)",
      "titleEn": "Poster (A4)",
      "descriptionBn": "",
      "descriptionEn": "",
      "file": "materials/posters/a4-bn.pdf",
      "mime": "application/pdf",
      "sizeBytes": 0,
      "language": "bn",
      "audience": ["PROMOTER", "PARTNER"]
    },
    {
      "id": "caption-whatsapp-bn",
      "category": "CAPTION",
      "type": "TEXT",
      "titleBn": "WhatsApp ক্যাপশন",
      "titleEn": "WhatsApp caption",
      "textBn": "... {{promoLink}} ...",
      "textEn": "... {{promoLink}} ...",
      "audience": ["PROMOTER", "PARTNER"]
    }
  ]
}
```
Categories: `VIDEO, POSTER, BANNER, IMAGE, LOGO, STORY, CAPTION, GUIDE`.

Rules:
- Validate manifests with Zod. Invalid/missing/unreachable manifest → use last-known-good cache; if none, hide the video section (hero renders normally) and log `MANIFEST_INVALID` (code only). NEVER break the home page.
- Fetch server-side with `revalidate` = `AppConfig.heroManifestRevalidateSec` (default 300).
- Append `?v=<manifest.version>` to media URLs for cache-busting. Replacing a file = upload same name + bump `version`.
- Set `Cache-Control: public, max-age=3600` on hero media; document it in the owner guide.
- Hero bucket needs CORS allowing the site origin (required for cross-origin `<track>` captions) and Range requests (seeking). Verify both.
- A language not in `variants` falls back to `defaultLanguage`. Video language is independent of UI locale; default to UI locale if a variant exists.
- Text templates: replace ONLY `{{promoLink}}` and `{{promoCode}}` server-side. No price/percent substitution, no money math (Decision 14).
- Do NOT hardcode prices, percentages or commission rates anywhere in Phase 11 content.

## E.4 Hero video UX & performance
- Hero order: search bar stays above the fold; the video card sits beside it on desktop and directly below on mobile. The video must never push search off the first screen.
- Initial render: poster via `next/image` + play button only. `<video preload="none">`. NEVER autoplay. The player is a client component loaded with `next/dynamic` on first tap/intent so the hero JS budget (<150KB gzipped, CLAUDE.md Sec 0 rule 8) holds.
- Quality: default 480; use 720 only if the user selects it or the connection is good (`navigator.connection` when available, honour `saveData`). Quality switch swaps `src` and preserves `currentTime`.
- Captions: `<track kind="subtitles">` per manifest entry with `crossorigin="anonymous"` on `<video>`. Caption menu; remember choice in `localStorage` (try/catch).
- Controls: native-style, keyboard accessible, ≥44px touch targets, visible focus, `prefers-reduced-motion` respected, captions toggle labelled in both languages.
- Errors: video error → localized message + retry. Slow network → poster stays, show spinner state.
- Lighthouse mobile ≥90 non-map must still pass with the hero video present. If not, STOP and report.

## E.5 Reactions, comments, share
**Prisma (Phase 11 migration; no PostGIS):**
```
enum HeroReactionType { LIKE LOVE INSPIRED }
enum HeroCommentStatus { VISIBLE PENDING HIDDEN }

model HeroReaction {
  id String @id @default(uuid())
  userId String
  videoKey String
  type HeroReactionType
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  @@unique([userId, videoKey])
  @@index([videoKey, type])
}

model HeroComment {
  id String @id @default(uuid())
  userId String
  videoKey String
  body String            // plain text, max AppConfig.heroCommentMaxLength
  status HeroCommentStatus @default(VISIBLE)
  reportCount Int @default(0)
  createdAt DateTime @default(now())
  deletedAt DateTime?
  @@index([videoKey, status, createdAt])
}
```
Extend the existing Report model/enum with a `HERO_COMMENT` target type (validate target exists and is VISIBLE; same polymorphic rules as CLAUDE.md Sec 7).

`videoKey` is the stable string from the manifest (`hero-explainer`), so reactions/comments survive video replacement.

**AppConfig keys (seed in Phase 11; never hardcode):**
`heroVideoEnabled=true, heroVideoReactionsEnabled=true, heroVideoCommentsEnabled=true, heroVideoCommentsRequireApproval=false, heroCommentAutoHideReports=3, heroCommentMaxLength=500, heroCommentPerHourLimit=5, heroManifestRevalidateSec=300, signedUrlTtlSec=300, materialsDownloadPerHourLimit=30`.

**Behaviour:**
- Anyone can watch and share. Reactions/comments require login (verified user, not `blocked`).
- One reaction per user per videoKey; changing type updates it; same type again removes it.
- Comments: plain text only, rendered escaped; strip/deny URLs and phone numbers (anti-spam); trim; length cap from config; rate-limited per user via Upstash (`heroCommentPerHourLimit`); show first name only (privacy). Users can soft-delete their own comment.
- If `heroVideoCommentsRequireApproval=true` new comments are `PENDING` and appear in the Phase 10 moderation queue; otherwise `VISIBLE`.
- Report button on every comment → increments `reportCount`; at `heroCommentAutoHideReports` → status `HIDDEN` and it appears in the Phase 10 moderation queue as type `HERO_COMMENT`. Admin can restore or delete there. This queue entry is the ONLY admin UI change in Phase 11.
- AuditLog: admin hide/restore/delete (`HERO_COMMENT_HIDE`, etc.). Allowlist logging only (ids, action, codes). Never log comment body or phone.
- Counts (reactions per type, comment count) cached ~60s; on failure hide counts, never error the page.
- Comments load lazily in a bottom sheet (mobile) / panel (desktop); focus trap, Escape closes, aria labels in both languages.
- Share menu: Web Share API when available; fallback buttons: WhatsApp (`wa.me/?text=`), copy link. Shared URL = `/[locale]/watch`. Promoters/Partners also see "Share with my link" that uses their promo link.

## E.6 `/[locale]/watch` page
- Server component: same player and reaction/comment UI, plus the language selector.
- SEO: `VideoObject` JSON-LD (name, description, thumbnail=poster, uploadDate, duration, contentUrl), OG tags with poster, `og:video` optional. Included in sitemap per locale, hreflang.
- If no manifest: 404-style "video coming soon" page, never a crash.

## E.7 Materials library & personal promo kit
- Route: `/[locale]/(dashboard)/materials`, linked from the Partner and Promoter dashboards.
- Access: `can(user, 'view', 'AD_MATERIALS')` in `lib/policy.ts`: role PROMOTER or PARTNER AND `kycStatus=VERIFIED` AND not blocked. Server-enforced on every action.
- List items from the private manifest grouped by category, filtered by `audience`, `language`, and locale. Show title/description in the current locale (fallback to the other language, never empty; `getLocalizedName` pattern from Decision 18).
- Download: server action issues a short-lived signed URL (`signedUrlTtlSec`), `Content-Disposition: attachment`. Rate-limited (`materialsDownloadPerHourLimit`). AuditLog `MATERIAL_DOWNLOAD` with allowlist `{userId, itemId}` only.
- The hero video files are also offered as a `VIDEO` category item (use the public hero URLs; download button uses `download` attribute).
- Text items: show with "Copy" button. `{{promoLink}}` = `https://ekota.store/p/<code>` built from the user's active PromoCode (PROMOTER or PARTNER type). `{{promoCode}}` = the code. No active code → show a localized "create your code first" message linking to code creation.
- Personal promo kit card: promo link, QR code (server-generated with the existing `qrcode` lib, error correction H, UTM `utm_source=promoter&utm_medium=qr`), copy and download buttons.
- A `GUIDE` item must always exist: "Claims guide" (the misconception table from Part C). Show a short notice above the library: do not promise guaranteed income, do not state delivery or payment guarantees, do not alter official materials' claims.

## E.8 i18n, accessibility, analytics
- All UI strings via next-intl in `messages/bn.json` + `en.json`. Missing string → English fallback + `missing-i18n.log`.
- WCAG AA: captions available, focus order, aria-live for reaction/comment status, 44px targets.
- Analytics events (no personal data): `hero_video_play`, `hero_video_25|50|75|100`, `hero_video_share`, `hero_video_lang_change`, `material_download`. Use the existing Plausible/PostHog.

## E.9 Security & robustness
- Zod on every action; rate limits; AuthZ via `can()` only; row-level checks.
- Comment text never rendered as HTML; no dangerouslySetInnerHTML.
- Signed URLs never logged. Private bucket keys never exposed to the client.
- Manifest paths must be validated against an allowlist prefix (`hero/` or `materials/`) and rejected if they contain `..`, a scheme, or a leading slash.
- Netlify: no module-level state; use Upstash for rate limits; keep functions fast (CLAUDE.md Part 4.1). Do not proxy video bytes through Netlify functions: the browser streams directly from the storage/CDN.

## E.10 Acceptance (all must pass before Phase 11 DONE)
1. No manifest / invalid manifest → home page renders normally, no video section, no console errors.
2. With a valid manifest: poster shows, video loads only after tap, seeking works (Range), captions toggle works cross-origin.
3. Language fallback works; adding a new language = new files + manifest entry only (test with a fixture).
4. Quality switch preserves playback position; `saveData` defaults to 480.
5. Replacing a file and bumping `version` serves the new file (cache-bust verified).
6. Logged-out user can watch/share but cannot react/comment (localized prompt to log in).
7. One reaction per user; toggle/change semantics correct (unique constraint test).
8. Comment rules: length cap, links/phones rejected, rate limit, own-delete, escaped rendering.
9. Reports: duplicate report by same user counted once; auto-hide at threshold; appears in Phase 10 queue; admin restore/delete audited.
10. `heroVideoCommentsEnabled=false` hides/disables comments; `heroVideoCommentsRequireApproval=true` produces PENDING comments.
11. Materials: unverified user, wrong role, and blocked user all get FORBIDDEN; verified Promoter/Partner can download; signed URL expires; audit log written; rate limit enforced.
12. `{{promoLink}}`/`{{promoCode}}` substitution correct; no active code case handled.
13. Manifest path-traversal fixtures (`../`, `https://`, leading `/`) rejected.
14. `/watch` has valid JSON-LD and OG tags; sitemap includes it.
15. Lighthouse mobile ≥90 on home with hero video present; hero JS budget respected.
16. No money math, no hardcoded prices/percentages in Phase 11 code or content. No PostGIS SQL in Phase 11 migration.
17. Self-Test Checklist (CLAUDE.md Part 0.4) all ticked, plus: "Did I build any admin panel/CMS or video upload UI? (must be NO)".

## E.11 Output after Phase 11
(a) file tree, (b) how to run/test, (c) acceptance checklist ticked, (d) known gaps, (e) 20-line PHASE_STATE update, (f) the owner guide (Part F) copied to `docs/OWNER_CONTENT_GUIDE.md`, (g) list of `BLOCKED-ON-HUMAN` items (e.g. video files not yet uploaded).

---

# PART F — আপনার জন্য: কনটেন্ট আপডেটের নিয়ম

## ভিডিও বদলানো
১. নতুন ভিডিও `video-480.mp4` ও `video-720.mp4` নামে এনকোড করুন (Part D-র কমান্ড)।
২. স্টোরেজ ড্যাশবোর্ডে (Supabase/R2) `hero/bn/` ফোল্ডারে একই নামে ফাইলগুলো আপলোড করুন, পুরোনোটা রিপ্লেস হয়ে যাবে।
৩. নতুন পোস্টার ও সাবটাইটেল (`.vtt`) থাকলে একইভাবে রিপ্লেস করুন।
৪. `hero/manifest.json` খুলে `version`-এর সংখ্যা ১ বাড়িয়ে সেভ করুন।
৫. ৫ মিনিটের মধ্যে সাইটে নতুন ভিডিও দেখা যাবে। কোনো কোড, ডিপ্লয় বা অ্যাডমিন প্যানেল লাগবে না।

## নতুন ভাষা যোগ
১. `hero/<ভাষা-কোড>/` ফোল্ডার বানিয়ে ভিডিও, পোস্টার, সাবটাইটেল রাখুন (উদাহরণ: `hero/en/`, `hero/ms/`)।
২. `hero/manifest.json`-এর `variants` তালিকায় ওই ভাষার একটি ব্লক যোগ করুন (Part E.3-র নমুনা দেখে), `version` বাড়ান।
৩. সাইটের নিজস্ব UI-ভাষা (বোতাম, লেবেল) যোগ করা আলাদা কাজ। শুধু ভিডিওর ভাষা যোগ করতে কোড লাগে না।

## প্রচার-সামগ্রী যোগ বা বদল
১. ফাইল `materials/<ধরন>/` ফোল্ডারে আপলোড করুন (প্রাইভেট বাকেট)।
২. `materials/manifest.json`-এ একটি নতুন `item` যোগ করুন (শিরোনাম বাংলা ও ইংরেজি, ফাইলের পথ, ধরন) এবং `version` বাড়ান।
৩. প্রমো লিঙ্কসহ ক্যাপশন চাইলে `TEXT` ধরনের আইটেমে `{{promoLink}}` লিখুন, প্রতিটি প্রচারকারী নিজের লিঙ্ক পাবেন।

## সতর্কতা
- `manifest.json` ভুল হলে সাইট ভাঙবে না, শুধু ভিডিও/লাইব্রেরি লুকিয়ে যাবে। সম্পাদনার পর একটি JSON ভ্যালিডেটর দিয়ে দেখে নিন।
- ফাইলের নাম বদলাবেন না। নাম বদলালে ম্যানিফেস্টেও বদলাতে হবে।
- ভিডিওতে বা সামগ্রীতে নির্দিষ্ট দাম, শতাংশ বা কমিশনের হার লিখবেন না।
- নতুন ভিডিওতেও কোনো মিউজিক থাকবে না, শেষে হেডফোনে একবার শুনে নিন।

---

# PART G — প্রকাশের আগের চেকলিস্ট
- [ ] ভিডিওতে মিউজিক, সুর, গুনগুন, নাশিদ বা আজান নেই (হেডফোনে শুনে যাচাই)।
- [ ] স্টক ফুটেজের নিজস্ব অডিও সরানো হয়েছে।
- [ ] ফ্রেমে কোনো মুখ, নির্দিষ্ট স্থানের নাম বা সাইনবোর্ড নেই।
- [ ] ভিডিওতে কোনো নির্দিষ্ট দাম, শতাংশ বা কমিশনের হার নেই।
- [ ] "ভুল ধারণা এড়ানোর নিয়ম" টেবিলের প্রতিটি সারি মানা হয়েছে।
- [ ] ইন্টারন্যাশনাল বিক্রয়কে চালু ফিচার হিসেবে বলা হয়নি।
- [ ] ভিডিও `faststart` সহ এনকোড করা, ৪৮০p ও ৭২০p দুটোই আছে।
- [ ] সাবটাইটেল সময়মতো মিলছে, UTF-8।
- [ ] ফুটেজের লাইসেন্স সংরক্ষিত।
- [ ] হিরো ভিডিওসহ হোম পেজে Lighthouse মোবাইল ≥৯০।
- [ ] কমেন্ট মডারেশন কাজ করছে (বা কমেন্ট বন্ধ রাখা হয়েছে)।
- [ ] প্রচার-সামগ্রী শুধু যাচাইকৃত Promoter/Partner ডাউনলোড করতে পারছেন।
# Selim AI Messenger — বাংলা সেটআপ

এটি Facebook **Page Messenger**-এর জন্য একটি starter app। এটি নিজে থেকে Facebook-এ লগইন করে না; Meta-এর অনুমোদিত Messenger Platform Webhook ও Send API ব্যবহার করে।

## কী করতে পারে
- Page-এ আসা text message webhook দিয়ে গ্রহণ করে
- OpenAI API দিয়ে বাংলাসহ উপযুক্ত ভাষায় উত্তর তৈরি করে
- Messenger Send API দিয়ে Page থেকে উত্তর পাঠায়

## যা লাগবে
1. একটি Facebook Page এবং সেটির admin/full-control access
2. Meta for Developers account ও Messenger permission-সহ app
3. HTTPS-সহ deploy করা server URL (লোকাল `localhost` Meta webhook হিসেবে কাজ করবে না)
4. Page Access Token
5. OpenAI API key (ChatGPT সাবস্ক্রিপশন থেকে আলাদা API billing হতে পারে)

## চালানোর নিয়ম
1. Node.js 20 বা নতুন সংস্করণ ইনস্টল করুন।
2. এই ফোল্ডারে terminal খুলে `npm install` চালান।
3. `.env.example` কপি করে `.env` নাম দিন।
4. `.env`-এ `VERIFY_TOKEN`, `PAGE_ACCESS_TOKEN`, `OPENAI_API_KEY` বসান।
5. `npm start` চালান।
6. সার্ভারটি HTTPS hosting-এ deploy করুন।
7. Meta Developer Dashboard → আপনার App → Messenger/Webhooks-এ callback URL দিন: `https://YOUR-DOMAIN/webhook`
8. Verify Token হিসেবে `.env`-এর `VERIFY_TOKEN`-এর একই মান দিন।
9. Page-এর `messages` webhook event subscribe করুন এবং Page-টি app-এর সঙ্গে যুক্ত করুন।

## নিরাপত্তা
- `.env` কখনো কাউকে পাঠাবেন না, GitHub-এ আপলোড করবেন না।
- Page Access Token বা OpenAI API key চ্যাটে শেয়ার করবেন না।
- Meta app review/permissions এবং messaging policy প্রযোজ্য। সাধারণত user-এর message-এর জবাবে অনুমোদিত messaging window-এর মধ্যে উত্তর দিতে হয়।
- আগে নিজের Page দিয়ে পরীক্ষা করুন। ব্যবহারকারীকে জানিয়ে দিন যে Page-এ AI উত্তর দিতে পারে।
- এই starter app text message সামলায়; ছবি, অডিও, handoff-to-human, rate limits, persistent logs এবং webhook signature verification production-এর আগে যোগ করা উচিত।

## গুরুত্বপূর্ণ সীমাবদ্ধতা
এই ZIP-টি source code; এটি এখনো আপনার Facebook Page-এ সংযুক্ত বা অনলাইনে deploy করা হয়নি। Meta token, OpenAI API key এবং hosting ছাড়া live auto-reply চালু হবে না।

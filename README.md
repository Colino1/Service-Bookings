# Bookline

Bookings, reminders and lost-money tracking for small businesses.

Small service businesses take most bookings in WhatsApp chats and lose revenue to no-shows and to customers who quietly stop returning. Bookline gives the owner one diary, one-tap reminders, and a running count of what missed bookings cost.

## Status
**Testing phase.** The files in this repository are an early, client-side version built to learn from real businesses. The full application, with customer self-booking, automatic notifications, cloud storage and payments, will be built when funding is available. The remaining work is listed in [Roadmap to the full app](#roadmap-to-the-full-app).

Current build: `2026-11-22h`

## Try it
- **Home page:** https://colino1.github.io/Service-Bookings/
- **App:** https://colino1.github.io/Service-Bookings/app.html
- **Demo with example businesses:** https://colino1.github.io/Service-Bookings/demo.html
- **No-show cost calculator:** https://colino1.github.io/Service-Bookings/calc.html

Open on a phone. There is nothing to install and no sign-up.

## How it works today
1. A customer taps the business's booking link, which opens a pre-filled WhatsApp message asking for service, day, time and name.
2. The owner agrees a time in WhatsApp and records it in Bookline. The service is chosen from a dropdown, and a missing service can be added inline.
3. Bookline generates confirmation, reminder, deposit-request and cancellation messages as WhatsApp deep links. The owner sends each with one tap.
4. After the booking the owner marks **Came** or **No-show**. Bookline computes earnings and money lost to no-shows.

## Feature status

| Capability | Testing build (today) | Full app (target) |
|---|---|---|
| Booking diary, list and month calendar | Available, stored in the browser | Synchronised across devices |
| Service catalogue with owner-set prices | Available | Available |
| Customer self-booking page with free times | Not available | Planned |
| Reminders (24 h and 2 h), confirmations, cancellations | One-tap WhatsApp links | Automatic delivery |
| Deposits | Tracking only: amount, request message, received flag | Online payment through a payment provider |
| Money board and no-show loss | Available | Available |
| Customer records, segments, birthday messages | Available | Available |
| Business report and growth tools | Available | Available |
| Data storage | Browser `localStorage`, manual backup | Managed database with automatic backup |
| Accounts and sign-in | None | Planned |
| Staff access and multiple locations | Not available | Planned |
| Subscription billing | Manual: payment on WhatsApp, access code issued by the owner | Automated billing |

## Architecture

**Testing build**
- Static HTML, CSS and JavaScript. No build step, no backend.
- State held in browser `localStorage`, with JSON export and import for backup.
- Messaging through `wa.me` deep links.
- Licence check performed client side with a signed access code. This is a deterrent for casual sharing, not a security control.
- Hosted on GitHub Pages.

**Target architecture**
- Progressive web app client.
- Managed PostgreSQL with row-level security for multi-tenant isolation.
- Authentication by email link or phone one-time code.
- Server-side scheduled jobs for notifications, and webhooks for payments.
- WhatsApp Business Platform for notifications, with SMS as fallback.
- A payment provider for deposits and subscription billing.
- Error tracking, uptime monitoring and automated backups.

## Roadmap to the full app
Items are grouped by workstream. They are listed in the order in which they unlock the product, not as dated commitments.

### 1. Backend and data layer
- [ ] Multi-tenant schema: businesses, services, customers, bookings, staff, availability
- [ ] Row-level security policies so each business can only read its own data
- [ ] Authentication by email link or phone one-time code, with session management
- [ ] Import path from the testing build's backup file
- [ ] Automated backups with point-in-time recovery

### 2. Customer self-booking
- [ ] Public booking page for each business at its own address
- [ ] Availability engine: working hours, breaks, slot length, buffers, minimum notice, holidays and blocked dates
- [ ] Concurrency-safe slot reservation, so two customers can never book the same time
- [ ] Customer cancellation and rescheduling through a signed link
- [ ] Abuse protection: CAPTCHA and rate limiting

### 3. Automatic notifications
- [ ] Scheduler for 24-hour and 2-hour reminders
- [ ] Automatic booking confirmations and cancellation notices
- [ ] WhatsApp Business Platform integration: business verification, message template approval, customer opt-in
- [ ] SMS fallback, including sender registration rules for each country
- [ ] Delivery status tracking, retries and opt-out handling

### 4. Payments and deposits
- [ ] Payment provider integration, with each business as the seller of record
- [ ] Webhook handling and payment reconciliation
- [ ] Refund and forfeited-deposit rules set by each business
- [ ] Automated subscription billing to replace manual access codes
- [ ] Legal and regulatory review for each country of operation

### 5. Teams and scale
- [ ] Staff accounts with roles and permissions
- [ ] Per-staff calendars and multi-location support
- [ ] Calendar export and sync (iCalendar feed, Google and Apple calendars)

### 6. Security, privacy and compliance
- [ ] Privacy policy, terms of service and recorded customer consent
- [ ] Data retention and deletion workflow
- [ ] Compliance review: Nigeria Data Protection Act, GDPR where applicable
- [ ] Encryption in transit and at rest, audit logging
- [ ] Independent security review

### 7. Internationalisation
- [ ] Interface translations and right-to-left support where needed
- [ ] Multi-currency pricing and formatting
- [ ] Time-zone-aware scheduling
- [ ] Local payment methods and messaging rules for each country

### 8. Quality and operations
- [ ] Automated unit and end-to-end tests
- [ ] Continuous integration and deployment, with a staging environment
- [ ] Error tracking, uptime monitoring and alerting
- [ ] Customer support tooling and documentation

### 9. Product and growth
- [ ] Installable app with offline support
- [ ] Guided onboarding and product analytics
- [ ] Referral programme and business-owner admin dashboard

## What funding is needed for
Cloud infrastructure, messaging and payment-provider fees, provider onboarding and verification, development and quality assurance, legal and compliance review, and customer support.

## Known limitations of the testing build
- Customers cannot choose a free time themselves. Bookings are recorded by the owner.
- Notifications are sent manually, one tap each.
- Data lives on a single device. Clearing browser data or changing phones removes it unless the owner has exported a backup.
- No accounts, no staff access and no payment processing.

## Privacy
The testing build has no server. Business data stays in the browser on the owner's own phone and is never transmitted to Bookline.

## Plans during testing
30 days free with everything included, then Bookline Pro at ₦2,000 per month in Nigeria or $5 per month elsewhere. Payment is arranged on WhatsApp and the owner receives an access code. These are testing-phase prices.

## Feedback
Use the **Send feedback** link on the home page. What testers report decides which roadmap items are built first.

## Hosting
Plain static files, deployed with GitHub Pages from the `main` branch, root folder.

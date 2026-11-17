# NotificationService

A small backend that sends emails and webhooks on a schedule. I kept needing "send a reminder at this time" in my other app ideas, so instead of writing it into every app I'm making one service they can all call.

> **Status:** built and tested locally. I'm cleaning it up and will upload the code soon.

## What it does

- Sends **emails** (SMTP) and **webhooks** (POSTs JSON to a URL)
- Send now or at a set time, with time zone support
- **Repeats** daily, weekly or monthly, with an optional end date
- **Retries** failed sends after 2 minutes, then 4, and marks them Failed after 3 attempts, keeping the error message
- **One API key per app**, so each app only sees its own notifications
- Cancel and retry endpoints, plus a health check

## How it works

An app sends a request like "email this person at 08:00 every Monday". The API saves it, and a background worker inside the API checks every few seconds and sends whatever is due. If sending fails it tries again later.

App ──POST──> API ──> SQLite <── Background worker ──> Email / Webhook

## Built with

.NET 10 · ASP.NET Core · EF Core · SQLite · BackgroundService · Swagger · xUnit

# issue-tracker

An issue tracker built with Next.js. Create issues, assign them to people, filter
and sort them, and see a summary on the dashboard.

[Live demo](https://issue-tracker-one-snowy.vercel.app)

## What it does

- Create, edit and delete issues, with a markdown editor for the description
- Every issue is OPEN, IN_PROGRESS or CLOSED
- Assign an issue to a signed-in user
- Filter the list by status, sort by column, page through results
- Dashboard with issue counts per status and a bar chart
- Sign in with Google

## Stack

| Area | Choice |
| --- | --- |
| Framework | Next.js, App Router |
| Language | TypeScript |
| Database | MySQL through Prisma |
| Auth | NextAuth, Google provider |
| UI | Radix UI Themes, Tailwind |
| Data fetching | React Query |
| Validation | Zod |
| Charts | Recharts |

## Data model

`Issue` holds the title, description, status and timestamps, plus an optional
relation to the `User` it is assigned to. NextAuth owns the `User`, `Account` and
`Session` tables.

## Running it locally

```bash
npm install
cp .env.example .env
```

Fill in the values:

- `DATABASE_URL`, pointing at a MySQL database
- `NEXTAUTH_URL`, which is `http://localhost:3000` in development
- `NEXTAUTH_SECRET`, any random string
- `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET`, from a Google OAuth client

Then set up the database and start the server:

```bash
npx prisma migrate dev
npm run dev
```

The app runs at http://localhost:3000.

## Notes

`/issues/new` and `/issues/edit/:id` need a signed-in user. That is handled in
`middleware.ts` rather than being repeated in each page.

Prisma runs with `relationMode = "prisma"`, so foreign keys are enforced by the
client rather than the database. That suits hosted MySQL providers that do not
support foreign key constraints.

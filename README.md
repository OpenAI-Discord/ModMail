This is a fork of: https://github.com/ChatSift/ModMail 

In accordance with the project's GNU AGPLv3 license, the following is a list of changes that were implemented:

- Adjusted docker-compose to work with M1 Silicon Chip
- Added a requirement that initial messages have more than 5 words 
- Added a system whereby snippets that have the same name as forum tags lead to the thread being automatically closed with the content of the snippet being sent

# modmail

## About

You can read all about the bot [here](https://didinele.notion.site/All-about-ChatSift-s-shiny-new-ModMail-ee2100f7438049bb96e141d05eaebb06).

## Self hosting

This repository contains source code for the bot itself under [packages/bot](./packages/bot/)
and for its HTTP API under [packages/api](./packages/api).
Self hosting the API is **unsupported and not recommended**,
and if you plan on exposing it to the internet you'll also need an instance of the
base ChatSift API, which can be found in the [dashboard repo](https://github.com/chatsift/dashboard).
It only offers CRUD over configuration and basic data as it's mostly intended for our dashboard.

A Docker image that can be used for running anything in this monorepo is available on DockerHub under `chatsift/modmail`.

---

With all those notices out of the way, the [docker-compose.yml](./docker-compose.yml) file
is probably the easiest way to get started.

Before you do anything else (even if you're using Docker), make sure to run `yarn --immutable`.
If you don't have yarn installed, `npm i -g yarn` (assuming you have a nodejs installation).

Simply create a new file called `.env`, follow the example from [.env.example](./.env.example),
and then `docker-compose build && docker-compose up -d`.

Now that the bot and postgres server are up, run `yarn deploy-commands` to register
the global slash commands, and then `yarn prisma migrate deploy` to get the database ready.

Alternatively, you can run your own postgresql instance, build the code with `yarn build`,
and start up the bot using `yarn start-bot`
in whatever way keeps it online (e.g. pm2).

---

## Updating a self-hosted instance

Assuming you're using Docker, you essentially just need to follow the steps above again.
`docker-compose build && docker-compose up -d`, re-deploy slash commands, and deploy prisma
migrations.

## Contributing/working on the project

- Set `NODE_ENV` env var to `dev`
	- If you're trying to figure out something wrong with cron jobs, `DEBUG_JOBS=true`.
- Forum thread titles default to DM content

## Licensing

This project is lincensed under the GNU AGPLv3 license. View the full file [here](./LICENSE).

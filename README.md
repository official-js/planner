# planner

## Contribution Rules

- Before starting to develop, make sure there is an issue discussing and approving the idea.
- Make sure to mention you are going to work on it, so that multiple people don't work on the same thing.
- Commits should be made with https://www.conventionalcommits.org/en/v1.0.0/

### Submitting a Pull Request

- Give the PR a descriptive title.
- No PR should be merged if that PR does not have fully tested code. Unit tests are much harder to add afterwards.
- Ensure all of the checks (lint and test) are passing.
- Any undocumented(currently in a pr) changes should be kept as a draft pr. Once the pr is merged by discord staff, we can mark it as ready for review and merge it. Certain changes can be merged ahead of time, if as a team we agree.

### Style Guide

- A function should not have more than 4 parameters. If more than 4 are needed, use an object.
- Try to keep low to no dependencies.
- Must use camel case (same property name as in the docs just in camel case).
- In typings, each field or property must be accompanied with a reasonable JSDoc comment right above its type definition. For example,

```ts
/** https://discord.com/developers/docs/resources/user#user-object */
export interface User {
  /** The user's id */
  id: string;
  /** The user's username, not unique across the platform */
  username: string;
  /** The user's 4-digit discord-tag */
  discriminator: string;
  /** The user's avatar hash */
  avatar: string | null;
  /** Whether the user belongs to an OAuth2 application */
  bot?: boolean;
  /** Whether the user is an Official Discord System user (part of the urgent message system) */
  system?: boolean;
  /** Whether the user has two factor enabled on their account */
  mfaEnabled?: boolean;
  /** The user's chosen language option */
  locale?: string;
  /** Whether the email on this account has been verified */
  verified?: boolean;
  /** The user's email */
  email?: string | null;
  /** The flags on a user's account */
  flags?: DiscordUserFlags;
  /** The type of Nitro subscription on a user's account */
  premiumType?: DiscordPremiumTypes;
  /** The public flags on a user's account */
  publicFlags?: DiscordUserFlags;
}
```

## Phase 1: Pre-Planning

- Discuss all possible choices in discord. As a decision is made as a group, we begin making issues for each aspect.
- Think of a name
- This is going to be the longest and hardest phase.

## Phase 2: Planning

- Split up each issue made in Phase 1 into smaller parts. For example, if the main issue was about rate limit handler, multiple issues can be made regarding this such as: how to support a fully standalone rest client, a class for buckets, a class for the manager itself, how to handle global rate limits, handling special edge cases like subrate limits which discord doesnt give headers for.
- Keep thinking of a name
- Move issues into Projects or Milestones whichever is preferred.

## Phase 3: Begin Coding

## Handlers

We need to have functions that will handle incoming ws events. For example, when a guild create event arrives, we need to create the guild structure and emit a guild event. These methods should be configurable, by allowing a user to override at will without having to fork and modify the lib.

Unit tests should be created for these events as well.

## REST Helpers

We need to have functions that will call the rest api. For example, a function that adds a role to the user.

## Rate Limiter

Create a bucket class. Create a subratelimit handler class. Create the actual rate limit manager. This should be ideally done in a way that it can be reused for different things for example, the websocket queu can also use this queue system.

## Typings

Build out all the typings for the api. Have typeguards where possible and opt for typeguard solutions and not generics.

## Utils

Create a collection class, Embed builder class, Interaction builder class, and any other utils that are necessary.

Anything from std should ideally be moved here into utils so that it is not a dependencies. For example if you need `await delay()` we should make a function

```ts
export function delay(ms: number) {
  return new Promise((res) =>
    setTimeout((): void => {
      res();
    }, ms)
  );
}
```

## Structures

The api should follow a vvery similar public api to discord.js. The internal code can be different but the public api for users should be same.

## Websockets

Implement all necessary functionality.

## Framework

A Klasa like framework but with a public api similar to akairo. Plugin capabilities.


# Delivery System - Applying API Mocks

This is a simplified freight calculator. It receives the names of an origin city
and a destination city, the weight and volume of the item, and returns the
delivery freight cost. The application queries a **location API** to get the
straight-line distance between the cities and uses this result in the freight
calculation.

## 1. Access

### 1.1. Opening the project in Stackblitz

First, open this project using the following link:

[![Open in Stackblitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/github/diego-aquino/api-mocking-app-delivery?startScript=dev&file=README.md)

This link will open the Stackblitz editor in your browser, similar to
[VS Code](https://code.visualstudio.com), install the dependencies, and start
the server.

On the left side, you will see the project folder structure, followed by an
editor and terminal in the center, and a mini-browser on the right side.

![Project opened in Stackblitz](./docs/images/project-opened-on-stackblitz.png)

In the upper left corner, click on "Fork" to save the project to your Stackblitz
profile. You will need to log in.

![Button to copy the project in Stackblitz](./docs/images/stackblitz-fork.png)

## 2. Project

This is a backend project that uses [Node.js](https://nodejs.org) with
[TypeScript](https://www.typescriptlang.org), [Fastify](https://fastify.dev),
[Axios](https://axios-http.com), and [Vitest](https://vitest.dev).

Important files:

- [`src/server/app.ts`](./src/server/app.ts): main application file where the
  server is implemented.
- [`src/clients/LocationClient.ts`](./src/clients/LocationClient.ts): class that
  makes HTTP calls to the location API.
- [`src/utils/shipping.ts`](./src/utils/shipping.ts): implementation of the
  freight calculation logic.
- [`tests/shipping.test.ts`](./tests/shipping.test.ts): file for freight
  calculation tests.

Useful commands:

- `npm install`: installs the **project dependencies** (automatically executed
  when opening the project in Stackblitz).
- `npm run dev`: starts the **server** in development mode.
- `npm run test`: runs the **application tests** in watch mode.
- `npm run types:check`: checks for **type errors** in the code.

The location API URL is declared in the [`.env.development`](./.env.development)
file. It is available in two versions:

| Version | URL                                    |
| ------- | -------------------------------------- |
| v1      | https://v1-location-d8b1dd3.vercel.app |
| v2      | https://v2-location-d8b1dd3.vercel.app |

> [!TIP]
>
> Access the links above to see the documentation for each version of the API.

## 3. Activity

### Part 1: Creating tests

In this first part, we will implement a test suite for this application. You
should use **one** of the two planned API mock tools,
[MSW](https://github.com/mswjs/msw) or
[Zimic](https://github.com/zimicjs/zimic), according to your pair's allocation
in the Delivery System
[in this spreadsheet](https://docs.google.com/spreadsheets/d/1fOp-6efUEp4KZx8UI9w0EuewHeWP1kIhWzWfViSihW0/edit?usp=sharing).

You should implement **four** test cases in the
[`tests/shipping.test.ts`](./tests/shipping.test.ts) file. The choice of which
aspects of the application to test is free, considering the following
guidelines:

1. All tests must make at least one request to the application.
2. All tests must exercise behaviors that use calls to the location API.
   However, the API should not be accessed directly in your tests, meaning all
   responses should be simulated by the mocks.
3. At least one test case must verify a successful response from the application
   (status codes
   [2XX](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#successful_responses)).
4. At least one test case must verify an error response from the application
   (status codes
   [4XX](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#client_error_responses)
   or
   [5XX](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#server_error_responses)).

To run the tests, use the command `npm run test`. With this command running, the
suite will be re-executed automatically when editing the application or tests.

![Running tests in Stackblitz](./docs/images/stackblitz-tests.png)

After implementing the cases described above, save the project sharing link. You
will need to submit it in the delivery form.

![Sharing the project in Stackblitz](./docs/images/stackblitz-sharing.png)

### Part 2: Migration to version 2 of the API

In this second part, we will migrate the project to use version 2 of the
location API, which has some changes compared to version 1.

Before starting, create a copy of the project you used in part 1. To do this,
click the "Fork" button in the upper corner. The goal is to keep the part 1
project unchanged and use a copy of it to migrate to version 2 of the API.

![Button to copy the project in Stackblitz](./docs/images/stackblitz-refork.png)

In the created copy, you should change the
[`.env.development`](./.env.development) file to use the URL of version 2 of the
API, updating the `LOCATION_API_URL` variable to the address below.

`.env.development`:

```bash
LOCATION_API_URL=https://v2-location-d8b1dd3.vercel.app
```

If the server or test command is running, you should restart them to read the
new URL.

Between versions 1 and 2 of the API, the following changes occurred:

- The `/cities/distances` route, where the origin and destination city
  identifiers were defined via query parameters, was changed to
  `/cities/:originCityId}/distances/cities/:destinationCityId`, moving the
  identifiers to route parameters;
- In the city return, the following fields were modified:
  - `stateName` and `stateCode` are now part of a `state` object, in the
    properties `state.name` and `state.code`, respectively.
  - `countryName` and `countryCode` are now part of a `country` object, in the
    properties `country.name` and `country.code`, respectively.

Now, you should adapt the tests and API mocks to handle these changes. To run
the suite, it is naturally necessary to also change the application and
integrate it with the new version of the API. In this activity, refactoring the
application is not mandatory, although it is recommended to check if the tests
are working correctly.

After making the adaptations, save the project sharing link used in this part 2.
You will also need to submit it in the delivery form, along with the link from
part 1.

## 4. Delivery

After completing the implementations in this application and in the
[Sharing System](https://github.com/diego-aquino/api-mocking-app-sharing), fill
out the delivery form with the links for parts 1 and 2. Confirm that all links
are publicly visible.

https://forms.gle/FP8gzzaBniawu6EV8

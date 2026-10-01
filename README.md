# panda-kernel-examples

Real-library adapter examples for [`@panda/kernel`](https://github.com/AdamPuzio/panda-kernel) — anything that needs an external dependency (a real `@panda/*` package, Express, MongoDB, a real npm-resolved module) lives here, not inside `@panda/kernel` itself.

See `@panda/kernel`'s own `examples/` for the small, dependency-free demos that stay there instead.

## Why this is a separate repo

`examples/` used to live inside `@panda/kernel` directly. That made it easy to reflexively couple kernel's own `package.json` to whatever an example happened to need — it happened twice (once with `express`, once with a test fixture package). Splitting examples out by dependency status fixes that structurally: kernel's own `package.json` never needs to know about anything these examples depend on.

## What's here

- `examples/adapters/real-command-entity.ts`, `real-colors-service.ts`, `real-trace-service.ts`, `real-logger-service.ts`, `real-task-entity.ts`, `real-scaffold-entity.ts` — wrap the real, unmodified `@panda/command`/`@panda/colors`/`@panda/trace`/`@panda/logger`/`@panda/task`/`@panda/scaffold` libraries behind the kernel entity contract.
- `examples/adapters/real-express-entity.ts`, `real-mongodb-entity.ts` — wrap real, external (non-Panda) libraries: Express and MongoDB.
- `examples/adapters/demo-express-module-nesting.ts` — proves contributing a route into a `panda:express` instance living inside an imported `panda:module`.
- `examples/demo-npm-module-resolution.ts` — proves real npm package resolution for `panda:module`, using [`@panda/example-auth-module`](https://github.com/AdamPuzio/panda-example-auth-module) as a real, installed test package.

Run any demo with `npx tsx <path>`. The Express demos need nothing extra; the MongoDB demo and the module-nesting-over-Express demo need a disposable MongoDB container (see the comments at the top of each file for the exact `docker run` command).

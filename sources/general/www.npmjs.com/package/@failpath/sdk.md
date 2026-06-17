# Source: https://www.npmjs.com/package/@failpath/sdk

# @failpath/sdk

![TypeScript icon, indicating that this package has built-in type declarations](https://static-production.npmjs.com/4a2a680dfcadf231172b78b1d3beb975.svg)

0.1.2 • Public • Published 3 days ago

- [Readme](https://www.npmjs.com/?activeTab=readme)
- [Code Beta](https://www.npmjs.com/?activeTab=code)
- [0 Dependencies](https://www.npmjs.com/?activeTab=dependencies)
- [0 Dependents](https://www.npmjs.com/?activeTab=dependents)
- [3 Versions](https://www.npmjs.com/?activeTab=versions)

# Failpath SDK

Record runtime step events for flows published with the Failpath CLI.

```shell
npm install @failpath/sdk
```

```ts
import { createFailpathClient } from "@failpath/sdk";

const failpath = createFailpathClient({
  projectKey: process.env.FAILPATH_PROJECT_KEY!,
});

export async function handleCheckout(requestId: string) {
  const run = failpath.run("checkout", { runId: requestId });

  const cart = await run.step("validate-cart", async () => {
    return validateCart();
  });

  await run.step("charge-card", async () => {
    return chargeCard(cart);
  });

  await failpath.flush();
}
```

`step()` queues a `running` event before the wrapped operation and then queues `success` or `error` when it finishes. Sends run in the background by default. Call `flush()` before a short-lived process exits, or pass a runtime `waitUntil` hook when available.

If the wrapped operation throws, the SDK records the error and rethrows the original application error.

## Typed flow keys

After running `npx failpath init`, `npx failpath sync`, or `npx failpath publish`, the CLI generates `.failpath/sdk.ts` from the current flow graph. Import it to autocomplete flow slugs and step keys.

```ts
import { createTypedFailpathClient, failpathFlows } from "../.failpath/sdk";

const failpath = createTypedFailpathClient({
  projectKey: process.env.FAILPATH_PROJECT_KEY!,
});

const run = failpath.run(failpathFlows.checkout.slug, { runId: "req_123" });

await run.step(failpathFlows.checkout.steps.validateCart, async () => {
  return validateCart();
});
```

The typed client also narrows string literals, so `failpath.run("checkout")` and `run.step("validate-cart", ...)` autocomplete when those keys exist in `.failpath/flows.json`.

## API

```ts
const failpath = createFailpathClient({
  projectKey: "fp_project_xxx",
  defaultMetadata: { environment: "production" },
});

const run = failpath.run("checkout", {
  runId: "req_123",
  metadata: { route: "/checkout" },
});

await run.step("validate-cart", () => validateCart(), {
  metadata: { cartId: "cart_123" },
});

await run.skip("send-receipt-email");

await failpath.recordStep({
  flowKey: "checkout",
  runId: "req_123",
  stepKey: "manual-step",
  status: "success",
});

await failpath.flush();
```

## Testing

Use the testing entrypoint to capture Failpath events in memory without sending requests during tests.

```ts
import { createMockFailpathClient } from "@failpath/sdk/testing";

const failpath = createMockFailpathClient();
```

## Options

- `projectKey`: Failpath project key.
- `endpoint`: optional development-only endpoint override. Defaults to `https://api.failpath.dev`.
- `enabled`: set to `false` to disable event sending.
- `defaultMetadata`: metadata merged into every event.
- `captureStack`: include error stacks. Defaults to `false`.
- `delivery`: telemetry delivery mode. Defaults to `"background"`. Use `"await"` to wait for each send before continuing.
- `throwOnSendError`: throw telemetry send errors. Defaults to `false`.
- `sendTimeoutMs`: maximum time to wait for each telemetry send. Defaults to `1500`. Set to `0` to disable the timeout.
- `maxQueueSize`: maximum queued background events before new events are dropped. Defaults to `1000`.
- `waitUntil`: optional hook for runtimes that can keep background promises alive after the handler returns.
- `onError`: callback for telemetry send errors.
- `fetch`: custom fetch implementation.

Do not send secrets, tokens, auth headers, full request bodies, payment data, or private customer data in metadata.

For deployed backends, set `FAILPATH_PROJECT_KEY` in the backend runtime environment. A repository `.env` file is enough for the Failpath CLI, but platforms such as Convex need their deployment env configured separately.

## Agent checklist

- Prefer `failpathFlows` from `.failpath/sdk.ts` for typed flow and step keys.
- If not using the generated helper, use `flow.slug` from `.failpath/flows.json` as the `run()` flow key.
- If not using the generated helper, use each node's `sdkStepKey` as the `step()` key.
- Reuse one `runId` for every step in the same request, job, or webhook.
- Wrap business steps, not tiny helpers or repository calls.
- Let application errors bubble. `step()` already rethrows the original error.

## Readme

### Keywords

none

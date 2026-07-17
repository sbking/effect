---
"effect": patch
---

Wake cluster storage reads at the next message `deliverAt` deadline, so scheduled messages are delivered when they become due instead of at the next poll interval tick.

`MessageStorage.unprocessedMessages` now returns `{ messages, nextDeliverAt }`, where `nextDeliverAt` is the earliest `deliverAt` deadline among the not-yet-due messages in the queried shards. `Sharding` uses it to schedule a single keyed wake per runner, clamped to the configured poll interval, and retains plain interval polling as the fallback if a storage read fails.

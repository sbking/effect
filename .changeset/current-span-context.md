---
"@effect/opentelemetry": minor
---

Fix `Tracer.currentOtelSpan` to work with OTLP module and add `Tracer.currentSpanContext`

`currentOtelSpan` now works with both the official OpenTelemetry SDK and the lightweight OTLP module. When using OTLP, it returns a read-only wrapper that provides `spanContext()` with the correct traceId, spanId, and traceFlags. The wrapper has no-op implementations for mutating methods since OTLP spans are managed differently.

Also added a convenience `currentSpanContext` API that directly returns `Otel.SpanContext` for cases where only the span context is needed.

Closes #5889

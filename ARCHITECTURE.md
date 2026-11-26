# Orin architecture

## Principles
- Local-first, no paid inference APIs.
- Python application logic; native C++/CUDA inference.
- Linux containers for CPU development and Jetson ARM64 deployment.
- Nemotron and Qwen interchangeable through a local inference adapter.
- OpenClaw orchestration; validated deterministic tools own state changes.
- SQLite persistent memory, independent of models; transactional writes and audit history.
- iPhone thin client for voice, text, photos and documents; Whisper and Piper run on server.
- No RAG unless a concrete retrieval requirement justifies it.
- Never commit personal data, secrets or model weights.

## Implementation sequence
1. Portable API and persistent shopping lists, with regression tests.
2. Tasks, contextual updates, undo and scheduling.
3. Local inference adapters and OpenClaw integration.
4. Voice and iPhone client.
5. Receipt OCR, document ingestion, weather and IPP printing.
6. Jetson benchmarks, security, backups and recovery.

## Constraints
Jetson has 8GB shared memory; benchmark one active model at a time. CPU tests do not establish GPU performance. Native iOS builds require macOS/Xcode. All external actions must be validated; uploaded content is untrusted. Production API requires authentication and encrypted transport.

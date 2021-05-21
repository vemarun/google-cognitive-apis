# Google Cognitive APIs

---

Selected Google Cloud APIs exposed via GRPC and REST:

* Dialogflow (NLP)
* Speech-to-text
* Text-to-speech

## Google API proto definitions
Google proto definitions have been taken from [this](https://github.com/googleapis/googleapis) repo.

## Limitations

* Only limited subset of Google cognitive APIs is supported. Feel free to raise PR with new additions! 
* For Dialogflow we currently support only SessionClient (The purpose of this library is not support different DialogFlow management APIs).
* REST APIs are supported with only purpose: to define structs that will enable deserialization of JSON config structures and their conversion into GRPC counterparts.
Full support for REST APIs will be not introduced.
* Dialogflow detect intent streaming (i.e. receiving audio data, performing speech-to-text followed by intent detection) is not fully supported.
It seems google APIs require half-close operation to be supported on audio stream to find out no more data will arrive and initiate intent detection.
Details can be found [here](https://cloud.google.com/dialogflow/es/docs/how/detect-intent-stream#detect-intent-stream-go).
Thus after streaming in all audio bytes API will simply timeout complaining data needs to be arriving promptly. If you know how to implement half-close with Rust/Tonic toolset let me know (raise PR/issue)!
Until then use streaming API and Dialogflow detect intent api separately to achieve the same result.

## Examples

You can find all examples [here](../examples).

### How to build

```rust
cargo build --examples
```

### How to run

```rust
cargo run --example recognizer_sync
```

```rust
cargo run --example recognizer_async
```

```rust
cargo run --example recognizer_streaming
```

```rust
cargo run --example recognizer_streaming_async_stream
```

```rust
cargo run --example sessions_client_streaming_detect_intent
```

```rust
cargo run --example sessions_client_streaming_detect_intent_async_stream
```

```rust
cargo run --example sessions_client_detect_intent
```

```rust
cargo run --example synthesizer
```
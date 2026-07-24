# 1.1.0-local

- Add separate Loon, Quantumult X, Shadowrocket, and Stash packages. Only the Surge package has been device-tested.
- Set `Type=Translate` as the default module mode and add complete Surge parameter descriptions.
- Add Chinese and English documentation, upstream attribution, installation steps, and known limitations.
- Add a six-second Translate fail-open deadline. Slow external translations now return the untouched source captions before iOS YouTube cancels its timedtext request.
- Remove Traditional Chinese from injected Auto translate entries so iOS displays Simplified Chinese only.
- Let the module's `Debug` parameter enable Surge's response-script diagnostics for Translate mode.
- Mark Official internal source-subtitle requests, delete `subtype`, and make the TimedText request script skip marked requests. This closes the request-side recursion path.
- Add `youtubei-att.googleapis.com` to Player/GetWatch regex and MITM.

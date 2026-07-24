# 1.0.3-local

- Add a six-second Translate fail-open deadline. Slow external translations now return the untouched source captions before iOS YouTube cancels its timedtext request.
- Remove Traditional Chinese from injected Auto translate entries so iOS displays Simplified Chinese only.
- Let the module's `Debug` parameter enable Surge's response-script diagnostics for Translate mode.
- Mark Official internal source-subtitle requests, delete `subtype`, and make the TimedText request script skip marked requests. This closes the request-side recursion path.
- Add `youtubei-att.googleapis.com` to Player/GetWatch regex and MITM.

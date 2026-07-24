# 1.0.2-local

- Set the Translate subtitle response-script timeout to 15 seconds; Surge defaults to 5 seconds, which is too short for some multi-part translations.
- Let the module's `Debug` parameter enable Surge's response-script diagnostics for Translate mode.
- Mark Official internal source-subtitle requests, delete `subtype`, and make the TimedText request script skip marked requests. This closes the request-side recursion path.
- Add `youtubei-att.googleapis.com` to Player/GetWatch regex and MITM.

# Allow Camera on non-localhost

For legacy reason, we test our application on a custon domain.

I thought I was in luck when I found: https://github.com/cypress-io/cypress/issues/5807

But to no avail.

Open you `/etc/hosts` file and add the following line:

```txt
# /etc/hosts

127.0.0.1    e2e.test
```

In a terminal serve the folder with `npm run serve`:

```bash
> npm run serve

> webcam-tests@ serve ~/Apps/webcam-tests
> http-serve

Starting up http-serve for ./
Available on:
  http://127.0.0.1:8080
  http://192.168.1.50:8080
Hit CTRL-C to stop the server

```

In another terminal run `yarn test`:

```
» npm run test

> webcam-tests@ test ~/Apps/webcam-tests
> ELECTRON_EXTRA_LAUNCH_ARGS='--unsafely-treat-insecure-origin-as-secure=http://e2e.test:8080' cypress run


====================================================================================================

  (Run Starting)

  ┌────────────────────────────────────────────────────────────────────────────────────────────────┐
  │ Cypress:    4.5.0                                                                              │
  │ Browser:    Electron 80 (headless)                                                             │
  │ Specs:      1 found (index.spec.js)                                                            │
  └────────────────────────────────────────────────────────────────────────────────────────────────┘


────────────────────────────────────────────────────────────────────────────────────────────────────

  Running:  index.spec.js                                                                   (1 of 1)


  1) should work

  0 passing (496ms)
  1 failing

  1) should work:
     Uncaught TypeError: Cannot read property 'getUserMedia' of undefined

This error originated from your application code, not from Cypress.

When Cypress detects uncaught errors originating from your application it will automatically fail the current test.

This behavior is configurable, and you can choose to turn this off by listening to the `uncaught:exception` event.

https://on.cypress.io/uncaught-exception-from-application
      at http://e2e.test:8080/index.html:42:32




  (Results)

  ┌────────────────────────────────────────────────────────────────────────────────────────────────┐
  │ Tests:        1                                                                                │
  │ Passing:      0                                                                                │
  │ Failing:      1                                                                                │
  │ Pending:      0                                                                                │
  │ Skipped:      0                                                                                │
  │ Screenshots:  1                                                                                │
  │ Video:        true                                                                             │
  │ Duration:     0 seconds                                                                        │
  │ Spec Ran:     index.spec.js                                                                    │
  └────────────────────────────────────────────────────────────────────────────────────────────────┘


  (Screenshots)

  -  ~/Apps/webcam-tests/cypress/screenshots/index.spec.js/should work (f     (1280x720)
     ailed).png


  (Video)

  -  Started processing:  Compressing to 32 CRF
  -  Finished processing: ~/Apps/webcam-tests/cypress/videos/index.spec.j    (0 seconds)
                          s.mp4


====================================================================================================

  (Run Finished)


       Spec                                              Tests  Passing  Failing  Pending  Skipped
  ┌────────────────────────────────────────────────────────────────────────────────────────────────┐
  │ ✖  index.spec.js                            484ms        1        -        1        -        - │
  └────────────────────────────────────────────────────────────────────────────────────────────────┘
    ✖  1 of 1 failed (100%)                     484ms        1        -        1        -        -

npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! webcam-tests@ test: `ELECTRON_EXTRA_LAUNCH_ARGS='--unsafely-treat-insecure-origin-as-secure=http://e2e.test:8080' cypress run`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the webcam-tests@ test script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
```

# FastBoot Meeting Notes 2016-05-11
## Attendees
_Please add yourself._
Tom Dale, Dan McClain, Ron White, Patrick Fisher, Arjan Singh, Krati Ahuja, Robert Jackson, Marco Otte-Witte, Hassan Abdel-Rahman
## Agenda
- [ ] Last Week's Action Items
  - [x] @kratiahuja to report on whether there is a significant performance regression 0.12 -> Node 4
  - [x] @tomdale to cut a new release with https://github.com/tildeio/htmlbars/pull/455
  - [ ] @rwjblue to write up constraints around steps to integrate `ember-cli-head` into `ember-cli`
  - [x] @danmcclain to deprecate `doc.title` prior to betas
- [x] Serializing server-side data for the client
- [x] Add version info to FastBoot package
- [x] Config in meta
- [x] Consensus on Redirect implementation
## Notes
- Discussed at core-team: Going to write all FB stuff in a node 4 compat way, then convert to node 0.12 compat with babel at publish time
  - Babel transpiled can be faster
- RJ: Working on ember-cli-head into ember-cli
- doc.title dep landed in 0.7.4
- Rename branch landed over weekend
  - express middleware is on beta 3
  - No beta branches yet
    - RJ: Do 3 branch method after 1.0 release
  - ember-cli-fastboot - 1.0 beta not released yet (Travis needs to pass)
    - https://github.com/ember-fastboot/ember-cli-fastboot/pull/190 needs to land prior to 1.0 beta
- Serialization server side
  - Need to take state on the server and have the same state on the browser render
    - example: Randomization on server and client
  - If you want state to be preserved between each render, put the data into the html and parse on client side
  - Core vs Addon
    - Seems important enough that many addons will want to take advantage of it
  - CSP issues with script tags (custom type)
    - May want to confirm inline scripts CSP header. Alternative is to use `<code>` block too
  - Meta tags have a limit on length
  - By adding a cache, we need deal with coordinating keys with service
  - Have separate `<script>` tags per namespace
    - Allows for more targeting parsing (Ember Data big payload vs some other addon that has a smaller payload)
  - Bikeshedding on the API language
    - Cutesy name makes the feature stick out and remove preconceptions
- Version information with compiled JS
  - Server can detect the version that the JS is compiled with
- Config in Meta
  - Stored in package.json now
  - APP_CONFIG wins over package.json
- Redirect Implementation
  - Always use 307 - Temporary redirect in FastBoot
    - Middleware would convert this if they need a 301
  - FastBootLocation
    - Include in `app/location/history` to override
    - include config to win with a FastBoot config
      - Seems like the better option so that it doesn't affect browser build
  - User perspective: nothing changes
    - transitionTo and replaceWith both do the same thing
## Action Items
- [ ] @tomdale to audit GitHub and npm packages  and make sure @danmcclain has access
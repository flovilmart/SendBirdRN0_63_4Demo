Sendbird SDK v4 - bundler issue
====

# How this project was generated?

The project was generated with the following command:

```
npx react-native init SendBirdRN0_63_4Demo --version 0.63.4
```

## Changes

- App.js: configure Sendbird and log instance

```typescript
import SendbirdChat from '@sendbird/chat';
import {OpenChannelModule} from '@sendbird/chat/openChannel';
const sb = SendbirdChat.init({
  appId: '123123',
  modules: [new OpenChannelModule()],
});
console.log(sb);
```

- Podfile: Disabled Flipper
- AppDelegate.m: Force URL for reaching out to the dev server

# Bundling issue

When requesting the non dev bundle with the minifier (sourceURLForBridge in AppDelegate.m)

`[NSURL URLWithString:@"http://localhost:8081/index.bundle?platform=ios&dev=false&minify=true"]`

We have the following issue:

```
2022-08-23 07:46:32.275551-0400 SendBirdRN0_63_4Demo[89340:39629584] [javascript] ReferenceError: Can't find variable: n
2022-08-23 07:46:32.300805-0400 SendBirdRN0_63_4Demo[89340:39629584] [javascript] Invariant Violation: Module AppRegistry is not a registered callable module (calling runApplication)
```

**ReferenceError: Can't find variable n**

This is the issue we also see in our project.

We determinted the bundler was at fault as latest version of Metro (0.70+) are producing valid production and dev builds with any minified config.

# Minifier issue

We also see a minifier issue in our project, while requesting any minified version.
**We cannot reproduce this issue with the current project.**

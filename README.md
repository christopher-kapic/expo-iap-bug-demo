This is to demonstrate a versioning error.

I get this error when I try to `npm run ios:device`:

```

```

Probably relevant files:

- package.json
- app.json
- ios/Podfile (generated - `platform :tvos, podfile_properties['ios.deploymentTarget'] || '15.1'`):

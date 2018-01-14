# Bug report for issue #3010

The code available in this repo reproduces the bug submitted in this [issue #3010](https://github.com/vuetifyjs/vuetify/issues/3010). To run the code simple do the following steps:

- clone the repo into your machine

```bash
$ git clone https://github.com/farrajota/vuetify-nuxt-issue-report.git
```

- cd to the dir and run the following commands

```bash
$ cd vuetify-nuxt-issue-report/
$ npm install && npm run generate
```

## Bug description

The issue revolves around using [v-tabs](https://next.vuetifyjs.com/components/tabs) to route to different views with the [nuxt](https://github.com/nuxt/nuxt.js/) framework.

When attempting to generate static files using the latest version of vuetify (`vuetify@1.0.0-beta.4`) it terminates the process with an error. Using the stable version (`vuetify@0.17.3`) works correctly.

Upgrading packages like `nuxt`, `vue` or any other package does not fix the issue (the error message clearly points that the problem come from the vuetify package itself).

> Note: `npm run dev` and `npm run build && npm run start` work correctly. It only raises an error when running `npm run generate`.

## Reproducing the error locally

Follow these steps to reproduce the error on your local machine:

1. Fetch the nuxt template using vuetify

```bash
vue init vuetifyjs/nuxt
```

2. cd to the project dir and install all dependencies

```bash
cd <proj> && npm install
```

3. Install vuetify 1.0.0-beta.4

```bash
npm install vuetify@1.0.0-beta.4 --save
```

4. Add the following code to layouts/default.vue

```
<template>
  <v-app dark>
    <!-- Add these 3 lines right after the first two tags in default.vue -->
    <v-tabs fixed-tabs centered>
      <v-tab router to="/">stuff</v-tab>
    </v-tabs>
    ...
```

5. Attempt to generate static files

```bash
npm run generate
```

## Error message

```bash
> nuxt generate

  ████████████████████ 100%

Build completed in 15.678s



 WARNING  Compiled with 1 warnings                       11:11:43

 warning

asset size limit: The following asset(s) exceed the recommended s
ize limit (300 kB).
This can impact web performance.
Assets:
  vendor.ea0247d362d4a7593cba.js (399 kB)

Hash: 3a0538249158632142d9
Version: webpack 3.10.0
Time: 15680ms
                                   Asset       Size  Chunks
              Chunk Names
 layouts/default.8a3bc2ed1e5d25810ede.js    2.63 kB       0  [emi
tted]         layouts/default
   pages/inspire.b3be5d62bb9901dc1c9e.js  692 bytes       1  [emitted]         pages/inspire
     pages/index.e9be0503ae250a5fff91.js    1.99 kB       2  [emitted]         pages/index
          vendor.ea0247d362d4a7593cba.js     399 kB       3  [emitted]  [big]  vendor
             app.f2b6b62a4ff38d03ba68.js    27.8 kB       4  [emitted]         app
        manifest.3a0538249158632142d9.js    1.58 kB       5  [emitted]         manifest
app.41dc6037a4e998209ea36ff7e56fb890.css     274 kB       4  [emitted]         app
                                LICENSES  645 bytes          [emitted]
 + 3 hidden assets

WARNING in asset size limit: The following asset(s) exceed the recommended size limit (300 kB).
This can impact web performance.
Assets:
  vendor.ea0247d362d4a7593cba.js (399 kB)
Hash: f518a6ea66ae69cd0e34
Version: webpack 3.10.0
Time: 7199ms
             Asset    Size  Chunks             Chunk Names
server-bundle.json  128 kB          [emitted]
[Vue warn]: Error in nextTick: "TypeError: Cannot read property 'firstChild' of undefined"

found in

---> <VTab>
       <VTabs>
         <VApp>
           <Default> at layouts/default.vue
             <Root>

 ERROR

  TypeError: Cannot read property 'firstChild' of undefined

  - vuetify.js:17404 VueComponent.<anonymous>
    [vuetify-nuxt-issue-report]/[vuetify]/dist/vuetify.js:17404:2    3

  - vue.runtime.common.js:1811 Array.<anonymous>
    [vuetify-nuxt-issue-report]/[vue]/dist/vue.runtime.common.js:    1811:12

  - vue.runtime.common.js:1732 flushCallbacks
    [vuetify-nuxt-issue-report]/[vue]/dist/vue.runtime.common.js:    1732:14



TypeError: Cannot read property 'firstChild' of undefined
    at VueComponent.<anonymous> (/home/mf/tmp2/vuetify/vuetify-nuxt-issue-report/node_modules/vuetify/dist/vuetify.js:17404:23)
    at Array.<anonymous> (/home/mf/tmp2/vuetify/vuetify-nuxt-issue-report/node_modules/vue/dist/vue.runtime.common.js:1811:12)
    at flushCallbacks (/home/mf/tmp2/vuetify/vuetify-nuxt-issue-report/node_modules/vue/dist/vue.runtime.common.js:1732:14)
    at <anonymous>
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! my_proj2@1.0.0 generate: `nuxt generate`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the my_proj2@1.0.0 generate script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

┌──────────────────────────────────────────────────────┐
│               npm update check failed                │
│         Try running with sudo or get access          │
│         to the local update config store via         │
│ sudo chown -R $USER:$(id -gn $USER) /home/mf/.config │
└──────────────────────────────────────────────────────┘

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/mf/.npm/_logs/2018-01-14T11_11_51_224Z-debug.log
```

## License

[MIT License](LICENSE)
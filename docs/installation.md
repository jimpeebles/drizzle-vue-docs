---
id: installation
title: Installation
sidebar_label: Installation
---

## Quick Start

To install Drizzle Vue Plugin, first create a Vue app within a Truffle project. See **[this example project](https://github.com/trufflesuite/drizzle-vue-plugin)** for a better understanding of how to structure your app. Make sure to install Vuex, as the Drizzle Vue Plugin hooks into a Vuex store.

Inside the root of your Vue app, run:

```js
npm install --save @drizzle/vue-plugin
```

Create a file called drizzleOptions.js in the root of your Vue app and add some configuration:

```js
// drizzleOptions.js

import SimpleStorage from "./contracts/SimpleStorage.json";
import ComplexStorage from "./contracts/ComplexStorage.json";
import TutorialToken from "./contracts/TutorialToken.json";

const options = {
  web3: {
    block: false,
    fallback: {
      type: "ws",
      url: "ws://127.0.0.1:9545"
    }
  },
  contracts: [SimpleStorage, ComplexStorage, TutorialToken],
  events: {
    SimpleStorage: ["StorageSet"]
  },
  polls: {
    accounts: 15000
  }
};

export default options;
```

The plugin comes packaged with several components that hook into Vuex, which allows your front end to communicate with Drizzle and interact with smart contracts.

Import the plugin in your main.js file or other entrypoint and add it to the Vue instance. Your file should look something like this:

```js
// main.js

import Vue from "vue";
import App from "./App.vue";
import Vuex from "vuex";

import drizzleVuePlugin from "@drizzle/vue-plugin";
import drizzleOptions from "./drizzleOptions";

Vue.use(Vuex);

const store = new Vuex.Store({ state: {} });

Vue.use(drizzleVuePlugin, { store, drizzleOptions });

new Vue({
  store,
  render: h => h(App)
}).$mount("#app");
```

You're now ready to use the plugin!

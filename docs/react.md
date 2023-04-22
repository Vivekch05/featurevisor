---
title: React SDK
description: Learn how to use Featurevisor SDK with React
---

Featureivisor also comes with an additional package for React.js, for ease of integration in your React.js application. {% .lead %}

## Installation

Install with npm:

```
$ npm install --save @featurevisor/react
```

## Setting up the provider

Use `FeaturevisorProvider` component to set up the SDK instance in your React application:

```jsx
import React from "react";
import ReactDOM from "react-dom";

import { createInstance } from "@featurevisor/sdk";
import { FeaturevisorProvider } from "@featurevisor/react";

const sdk = createInstance({
  datafileUrl: "https://cdn.yoursite.com/datafile.json"
});

ReactDOM.render(
  <FeaturevisorProvider sdk={sdk}>
    <App />
  </FeaturevisorProvider>,
  document.getElementById("root")
);
```

## Hooks

The package comes with several hooks to use in your components:

### useStatus

Know if the SDK is ready to be used:

```jsx
import React from "react":
import { useStatus } from "@featurevisor/react";

function MyComponent(props) {
  const { isReady } = useStatus();

  if (!isReady) {
    return <p>Loading...</p>;
  }

  return <p>SDK is ready</p>;
};
```

### useVariation

Get a feature's evaluated variation:

```jsx
import React from "react":
import { useVariation } from "@featurevisor/react";

function MyComponent(props) {
  const featureKey = "myFeatureKey";
  const attributes = { userId: "123" };

  const variation = useVariation(featureKey, attributes);

  if (variation === "b") {
    return <p>B variation</p>;
  }

  if (variation === "c") {
    return <p>C variation</p>;
  }

  // default
  return <p>Default experience</p>;
};
```

### useVariable

Get a feature's evaluated variable value:

```jsx
import React from "react":
import { useVariable } from "@featurevisor/react";

function MyComponent(props) {
  const featureKey = "myFeatureKey";
  const variableKey = "color";
  const attributes = { userId: "123" };

  const colorValue = useVariable(featureKey, variableKey, attributes);

  return <p>Color: {colorValue}</p>;
};
```

### activateFeature

Same as `useVariation`, but it will also bubble an activation event up to the SDK for tracking purposes.

This should ideally be only called once per feature, and only when we know the feature has been exposed to the user.
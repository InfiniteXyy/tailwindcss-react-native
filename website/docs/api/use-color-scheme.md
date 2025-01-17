---
title: useColorScheme()
sidebar_label: useColorScheme()
---

useColorScheme() provides access to the devices color scheme.

| Value          | Description                                                                                      |
| -------------- | ------------------------------------------------------------------------------------------------ |
| colorScheme    | The current device colorScheme                                                                   |
| setColorScheme | Override the current colorScheme with a different scheme (accepted values are `light` or `dark`) |

If you do not use to use the device's current color scheme, you can provide an initial color scheme to the [TailwindProvider](./tailwind-provider) via the `initialColorScheme` prop.

```tsx
import { useColorScheme } from "tailwindcss-react-native";
import { Text } from "react-native";

function MyComponent() {
  const { colorScheme, setColorScheme } = useColorScheme();

  return (
    <Text
      onPress={() => setColorScheme(colorScheme === "light" ? "dark" : "light")}
    >
      {`The color scheme is ${colorScheme}`}
    </Text>
  );
}
```

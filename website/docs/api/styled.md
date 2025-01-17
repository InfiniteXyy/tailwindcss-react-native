---
title: styled()
sidebar_label: styled()
---

## Usage

`styled()` is a [Higher-Order Component](https://reactjs.org/docs/higher-order-components.html) which allows your component to accept either the `tw` or `className` props. These props are compiled into StyleSheet objects and passed to your component via the `style` prop.

There is no difference between `tw` and `className`, but `tw` has priority.

```tsx
import { Text } from "react-native";
import { styled } from "tailwindcss-react-native";

const StyledText = styled(Text);

export function MyComponent() {
  return (
    <>
      <StyledText tw="font-bold">Hello world</StyledText>
      <StyledText className="font-bold">Hello world</StyledText>
    </>
  );
}
```

## Styling multiple properties

`styled()` can optionally accept a list of additional props to parse into runtime styles.

```tsx
function Wrapper({ innerStyle, children, ...props }) {
  return (
    <View {...props}>
      <View style={innerStyle}>
        { children }
      </View>
    </View>
  )
}

const StyledWrapper = styled(Wrapper, { props: ["innerStyle"] })

<StyledWrapper className="h-4" innerStyle="p-4"><Text>Hello, World!</Text></StyledWrapper>
```

## Mixing between inline props and CSS classes

Some components can either accept a value as a prop or be styled by CSS. An example is `react-native-svg` which provides as `fill` prop, but can also accept a class providing `fill` styling.

You can flag a components props as `classProps` to ensure the best output is used.

```tsx
import { styled } from "tailwindcss-react-native"
import { Svg, Rect } from "react-native-svg"

const StyledRect = styled(Rect, { classProps: ["fill", "stroke"]})

function MyStyledSvg({ stroke, ...props }) {
  return (
    <Svg height="100" width="100" {...props }>
      <StyledRect x="0" y="0" width="100" height="100" fill={fill} stroke={stroke} />
    </Svg>
  )
}

<MyStyledSvg fill="fill-black" stroke="stroke-2 stroke-blue-500" />
```

## Styling props that only accept values

Not all libraries use style objects, with many accepting single values as a props. You can use `spreadProps` to help style these components. At runtime, `spreadProps` will remove those props and replace them with the computed styles "spread" as props.

```tsx
import { ActivityIndicator } from "react-native";
import { styled } from "tailwindcss-react-native"

const StyledActivityIndicator = styled(ActivityIndicator, {
  spreadProps: ["color"]
})

<StyledActivityIndicator color="color-blue-500" />
```

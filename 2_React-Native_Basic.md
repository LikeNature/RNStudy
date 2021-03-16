# React-Native 기초

## 핵심 구성 요소 [#](https://reactnative.dev/docs/intro-react-native-components#core-components)

React Native에는 양식 제어에서 활동 표시기에 이르기까지 모든 것에 대한 많은 핵심 구성 요소가 있습니다. [API 섹션에서](https://reactnative.dev/docs/components-and-apis) 모두 [문서화되어 있습니다](https://reactnative.dev/docs/components-and-apis) . 주로 다음 핵심 구성 요소로 작업합니다.

| 네이티브 UI 구성 요소 반응 | ANDROID보기    | IOS보기          | 웹 아날로그             | 기술                                                         |
| :------------------------- | :------------- | :--------------- | :---------------------- | :----------------------------------------------------------- |
| `<View>`                   | `<ViewGroup>`  | `<UIView>`       | 스크롤하지 않는 `<div>` | 플렉스 박스, 스타일, 일부 터치 처리 및 접근성 컨트롤이있는 레이아웃을 지원하는 컨테이너 |
| `<Text>`                   | `<TextView>`   | `<UITextView>`   | `<p>`                   | 텍스트 문자열을 표시, 스타일 및 중첩하고 터치 이벤트도 처리합니다. |
| `<Image>`                  | `<ImageView>`  | `<UIImageView>`  | `<img>`                 | 다양한 유형의 이미지를 표시합니다.                           |
| `<ScrollView>`             | `<ScrollView>` | `<UIScrollView>` | `<div>`                 | 여러 구성 요소 및보기를 포함 할 수있는 일반 스크롤 컨테이너  |
| `<TextInput>`              | `<EditText>`   | `<UITextField>`  | `<input type="text">`   | 사용자가 텍스트를 입력 할 수 있습니다.                       |

## Layout with Flexbox

A component can specify the layout of its children using the Flexbox algorithm. Flexbox is designed to provide a consistent layout on different screen sizes.

You will normally use a combination of `flexDirection`, `alignItems`, and `justifyContent` to achieve the right layout.

> Flexbox works the same way in React Native as it does in CSS on the web, with a few exceptions. The defaults are different, with `flexDirection` defaulting to `column` instead of `row`, `alignContent` defaulting to `flex-start` instead of `stretch`, `flexShrink` defaulting to `0` instead of `1`, the `flex` parameter only supporting a single number.

### Flex [#](https://reactnative.dev/docs/flexbox#flex)

[`flex`](https://reactnative.dev/docs/layout-props#flex) will define how your items are going to **“fill”** over the available space along your main axis. Space will be divided according to each element's flex property.

In the following example, the red, yellow, and green views are all children in the container view that has `flex: 1` set. The red view uses `flex: 1` , the yellow view uses `flex: 2`, and the green view uses `flex: 3` . **1+2+3 = 6**, which means that the red view will get `1/6` of the space, the yellow `2/6` of the space, and the green `3/6` of the space.

### Flex Direction[#](https://reactnative.dev/docs/flexbox#flex-direction)

[`flexDirection`](https://reactnative.dev/docs/layout-props#flexdirection) controls the direction in which the children of a node are laid out. This is also referred to as the main axis. The cross axis is the axis perpendicular to the main axis, or the axis which the wrapping lines are laid out in.

- `column` (**default value**) Align children from top to bottom. If wrapping is enabled, then the next line will start to the right of the first item on the top of the container.
- `row` Align children from left to right. If wrapping is enabled, then the next line will start under the first item on the left of the container.
- `column-reverse` Align children from bottom to top. If wrapping is enabled, then the next line will start to the right of the first item on the bottom of the container.
- `row-reverse` Align children from right to left. If wrapping is enabled, then the next line will start under the first item on the right of the container.



### Layout Direction[#](https://reactnative.dev/docs/flexbox#layout-direction)

Layout direction specifies the direction in which children and text in a hierarchy should be laid out. Layout direction also affects what edge `start` and `end` refer to. By default, React Native lays out with LTR layout direction. In this mode `start` refers to left and `end` refers to right.

- `LTR` (**default value**) Text and children are laid out from left to right. Margin and padding applied to the start of an element are applied on the left side.
- `RTL` Text and children are laid out from right to left. Margin and padding applied to the start of an element are applied on the right side.

### Justify Content[#](https://reactnative.dev/docs/flexbox#justify-content)

[`justifyContent`](https://reactnative.dev/docs/layout-props#justifycontent) describes how to align children within the main axis of their container. For example, you can use this property to center a child horizontally within a container with `flexDirection` set to `row` or vertically within a container with `flexDirection` set to `column`.

- `flex-start`(**default value**) Align children of a container to the start of the container's main axis.
- `flex-end` Align children of a container to the end of the container's main axis.
- `center` Align children of a container in the center of the container's main axis.
- `space-between` Evenly space off children across the container's main axis, distributing the remaining space between the children.
- `space-around` Evenly space off children across the container's main axis, distributing the remaining space around the children. Compared to `space-between`, using `space-around` will result in space being distributed to the beginning of the first child and end of the last child.
- `space-evenly` Evenly distribute children within the alignment container along the main axis. The spacing between each pair of adjacent items, the main-start edge and the first item, and the main-end edge and the last item, are all exactly the same.

### Align Items[#](https://reactnative.dev/docs/flexbox#align-items)

[`alignItems`](https://reactnative.dev/docs/layout-props#alignitems) describes how to align children along the cross axis of their container. Align items is very similar to `justifyContent` but instead of applying to the main axis, `alignItems` applies to the cross axis.

- `stretch` (**default value**) Stretch children of a container to match the `height` of the container's cross axis.
- `flex-start` Align children of a container to the start of the container's cross axis.
- `flex-end` Align children of a container to the end of the container's cross axis.
- `center` Align children of a container in the center of the container's cross axis.
- `baseline` Align children of a container along a common baseline. Individual children can be set to be the reference baseline for their parents.

> For `stretch` to have an effect, children must not have a fixed dimension along the secondary axis. In the following example, setting `alignItems: stretch` does nothing until the `width: 50` is removed from the children.

### Align Self[#](https://reactnative.dev/docs/flexbox#align-self)

[`alignSelf`](https://reactnative.dev/docs/layout-props#alignself) has the same options and effect as `alignItems` but instead of affecting the children within a container, you can apply this property to a single child to change its alignment within its parent. `alignSelf` overrides any option set by the parent with `alignItems`.

### Align Content[#](https://reactnative.dev/docs/flexbox#align-content)

[alignContent](https://reactnative.dev/docs/layout-props#aligncontent) defines the distribution of lines along the cross-axis. This only has effect when items are wrapped to multiple lines using `flexWrap`.

- `flex-start` (**default value**) Align wrapped lines to the start of the container's cross axis.
- `flex-end` Align wrapped lines to the end of the container's cross axis.
- `stretch` (*default value when using Yoga on the web*) Stretch wrapped lines to match the height of the container's cross axis.
- `center` Align wrapped lines in the center of the container's cross axis.
- `space-between` Evenly space wrapped lines across the container's cross axis, distributing the remaining space between the lines.
- `space-around` Evenly space wrapped lines across the container's cross axis, distributing the remaining space around the lines. Compared to `space-between`, using `space-around` will result in space being distributed to the beginning of the first line and the end of the last line.

### Flex Wrap[#](https://reactnative.dev/docs/flexbox#flex-wrap)

The [`flexWrap`](https://reactnative.dev/docs/layout-props#flexwrap) property is set on containers and it controls what happens when children overflow the size of the container along the main axis. By default, children are forced into a single line (which can shrink elements). If wrapping is allowed, items are wrapped into multiple lines along the main axis if needed.

When wrapping lines, `alignContent` can be used to specify how the lines are placed in the container. Learn more [here](https://yogalayout.com/docs/flex-wrap).

### Flex Basis, Grow, and Shrink[#](https://reactnative.dev/docs/flexbox#flex-basis-grow-and-shrink)

- [`flexBasis`](https://reactnative.dev/docs/layout-props#flexbasis) is an axis-independent way of providing the default size of an item along the main axis. Setting the `flexBasis` of a child is similar to setting the `width` of that child if its parent is a container with `flexDirection: row` or setting the `height` of a child if its parent is a container with `flexDirection: column`. The `flexBasis` of an item is the default size of that item, the size of the item before any `flexGrow` and `flexShrink` calculations are performed.

- [`flexGrow`](https://reactnative.dev/docs/layout-props#flexgrow) describes how any space within a container should be distributed among its children along the main axis. After laying out its children, a container will distribute any remaining space according to the flex grow values specified by its children.

  `flexGrow` accepts any floating point value >= 0, with 0 being the default value. A container will distribute any remaining space among its children weighted by the children’s `flexGrow` values.

- [`flexShrink`](https://reactnative.dev/docs/layout-props#flexshrink) describes how to shrink children along the main axis in the case in which the total size of the children overflows the size of the container on the main axis. `flexShrink` is very similar to `flexGrow` and can be thought of in the same way if any overflowing size is considered to be negative remaining space. These two properties also work well together by allowing children to grow and shrink as needed.

  `flexShrink` accepts any floating point value >= 0, with 0 being the default value (on the web, the default is 1). A container will shrink its children weighted by the children’s `flexShrink` values.

### Width and Height[#](https://reactnative.dev/docs/flexbox#width-and-height)

The `width` property specifies the width of an element's content area. Similarly, the `height` property specifies the height of an element's content area.

Both `width` and `height` can take the following values:

- `auto` (**default value**) React Native calculates the width/height for the element based on its content, whether that is other children, text, or an image.
- `pixels` Defines the width/height in absolute pixels. Depending on other styles set on the component, this may or may not be the final dimension of the node.
- `percentage` Defines the width or height in percentage of its parent's width or height, respectively.

### Going Deeper[#](https://reactnative.dev/docs/flexbox#going-deeper)

Check out the interactive [yoga playground](https://yogalayout.com/playground) that you can use to get a better understanding of flexbox.

We've covered the basics, but there are many other styles you may need for layouts. The full list of props that control layout is documented [here](https://reactnative.dev/docs/layout-props).

Additionally, you can see some examples from [Wix Engineers](https://medium.com/wix-engineering/the-full-react-native-layout-cheat-sheet-a4147802405c).

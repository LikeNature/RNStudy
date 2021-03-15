# Clone-Project

## App.js

 - `<Status Bar barStyle="dark-content" />`
   - `<SafeAreaView >`
     - `<ScrollView >`
       - `<Header />`
       - `<View />`
       - `<View />`
         - `<View />`
           - `<Text />`
           - `<Text />`
             - `<Text />`
         - `<View />`
           - `<Text />`
           - `<Text />`
             - `<ReloadInstructions />`
         - `<View />`
           - `<Text />`
           - `<Text />`
         - `<LearnMoreLinks />`
           - .\SampleApp\node_modules\react-native\Libraries\NewAppScreen\components\LearnMoreLinks.js
           - 위 경로에서 소스 수정

### const App: () => React$Node = () => {...}  

- I'm using [flow](https://flow.org/en/) with vscode but had the same problem. I solved it with these steps:
  1. Install the extension [Flow Language Support](https://marketplace.visualstudio.com/items?itemName=flowtype.flow-for-vscode)
  2. Disable the built-in TypeScript extension:
     1. Go to *Extensions* tab
     2. Search for **@builtin TypeScript and JavaScript Language Features**
     3. Click on *Disable*








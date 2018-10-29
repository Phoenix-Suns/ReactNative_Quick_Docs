# Đa Ngôn Ngữ

https://react.i18next.com/getting-started

## Cài đặt:

> npm install react-i18next --save

## Setup:

### App.js

```js
import React, {Component} from 'react';
import { I18nextProvider, translate } from 'react-i18next';
import { Provider } from 'react-redux';
import ConfigI18next from './src/locales/index';
import StackMain from './src/navigators/StackMain';
import AppStore from './src/redux/AppStore';

// Main Component
const WrappedStack = ({ t }) => {
  console.disableYellowBox = true;  // Disable Warning Box
  return (
    /* Store Redux */
    <Provider store={AppStore}>
        {/* Stack Navigation */}
        <StackMain screenProps={{ t }} />
    </Provider>
  );
};

const ReloadAppOnLanguageChange = translate('common', {
  bindI18n: 'languageChanged',
  bindStore: false,
})(WrappedStack);

type Props = {};
export default class App extends Component<Props> {
  render() {
    return (
      <I18nextProvider i18n={ConfigI18next}>
        <ReloadAppOnLanguageChange />
      </I18nextProvider>
    );
  }
}
```

### ConfigI18next.js

```js
import i18next from 'i18next';
import { reactI18nextModule } from 'react-i18next';
import en from './en.json';
import vn from './vn.json';

const ConfigI18next = i18next
  // .use(languageDetector)
  .use(reactI18nextModule)
  .init({
    fallbackLng: 'en',
    resources: { en, vn },

    // have a common namespace used around the full app
    ns: ['common'],
    defaultNS: 'common',

    debug: true,

    // cache: {
    //  enabled: true
    // },

    interpolation: {
      escapeValue: false, // not needed for react as it does escape per default to prevent xss!
    },
  });

export default ConfigI18next;
```

### en.json

```json
{
  "home-page": {
    "title": "Welcome Message"
  },
  "common": {
    "Username": "User name",
    "Password": "Password",
    "Error": "Error",
    "Login": "Login",
    "OK": "OK",
  }
}
```

### TestChangeText.js

```js
import React, { PureComponent } from 'react';
import { View, Text, Button } from 'react-native';
import { translate, Trans } from 'react-i18next';

class TestI18next extends PureComponent {
  changeLanguage = (lng) => {
    console.log(lng);
    this.props.i18n.changeLanguage(lng);
  };

  render() {
    const { t, i18n, navigation } = this.props;

    return (
      <View>
        <Text>{t('Username')}</Text>
        <Button title="change" onPress={() => { this.changeLanguage('vn'); }} />
      </View>
    );
  }
}

export default translate(['common'], { wait: true })(TestI18next);
```

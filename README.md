# universal-cookie (Fork of [react-cookie](https://github.com/eXon/react-cookie))
Load, save and remove cookies within your React application.

**Thanks to [eXon](https://github.com/eXon) for laying the groundwork. I forked this project because I have a different preferences for coding style (I prefer ES6 / mocha to ES5 / jasmine) and am using cookies heavily in a few applications.**


## Universal Cookies

`universal-cookie` can be used from the client and server sides. From server code, you can use `const dispose = cookie.use(req, res)` to have cookie logic operate on an in-transit connections response cookie headers. *(require the cookieParser middleware)*

To ensure long running async operations do not attempt to write to cookies after the request has been sent, you may call the `dispose` function that is returned prior to returning the response from your connect-style middleware.

You can also set the raw cookie directly via `cookie.setRawCookie(req.headers.cookie)`


## Install

`npm install universal-cookie`

# Examples

```js
import { Component } from 'react';
import cookie from 'react-cookie';

export default class MyApp extends Component {
  constructor(props) {
    super(props);
    this.state = { userId: cookie.load('userId') };
  }

  onLogin(userId) {
    this.setState({ userId });
    cookie.save('userId', userId, { path: '/' });
  }

  onLogout() {
    cookie.remove('userId', { path: '/' });
  }

  render() {
    return (
      <LoginPanel onSuccess={this.onLogin.bind(this)} />
    );
  }
}
```
## Usage

### `reactCookie.load(name, [doNotParse])`
### `reactCookie.save(name, val, [opt])`
### `reactCookie.remove(name, [opt])`
### `reactCookie.plugToRequest(req, res): unplug()`
### `reactCookie.setRawCookie(cookies)`

## opt
Support all the cookie options from the RFC.

### path
> cookie path

### expires
> absolute expiration date for the cookie (Date object)

### maxAge
> relative max age of the cookie from when the client receives it (seconds)

### domain
> domain for the cookie

### secure
> true or false

### httpOnly
> true or false

## License
This project is under the MIT license. You are free to do whatever you want with it.

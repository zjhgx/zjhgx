## Account Kit
Account Kit 的登录流程集帐户注册和帐户登录为一体。无需检查帐户是否已经存在，也无需创建单独的新用户注册流程。登录或注册成功后，Account Kit 会向您的应用提供登录用户的验证凭证。

### 访问口令
An access token returned from the SDK allows you to verify the authenticity of a user's identity on the server side when processing requests for your application.<br>
通过由 SDK 返回的访问口令，您可以在处理应用请求时从服务器端验证用户的身份。
 * 成功的登录会创建一个帐户编号和关联的访问口令。A successful login creates an Account ID and an associated access token.
* 访问口令可用于访问 Account Kit REST API。The access token can be used to access Account Kit REST APIs.
* 您应该将访问口令传递至应用的服务器，用于验证用户身份。You should pass the access token to your application's server to verify the user's identity.
It's a good practice to include the access token with every server request to your application and to verify the user ID from the token and not directly from the client. This helps protect your application from unauthorized uses.

##### 用户访问口令
User Access Tokens are obtained through the SDKs after a successful login. For the Android and iOS SDK, the access token also can be retrieved by calling the getCurrentAccessToken method while the session is still active.

##### App Access Tokens
App Access Tokens allow you to make server calls on behalf of your application. These are useful for account management operations that a user may not have access to, such as reading a list of all users, and for protecting the initial login request.<br>
App access tokens are the concatenation of your app ID and your Account Kit app secret. They take the form AA|<facebook_app_id>|<app_secret><br>
You should not store your app secret on a mobile device, so these are reserved for server to server calls.

##### Access Token Validation
When your app makes API calls to your server, validate the user's identity by verifying their access token. The User Access Token is available from each SDK while a user is logged in. Validate a User Access Token by accessing the Account Kit API on the Account ID edge and passing the User Access Token as a parameter.<br>

```
GET https://graph.accountkit.com/v1.3/me/?access_token=<access_token>
```
This returns the Account ID associated with this User Access Token if it's valid.This response also includes the current associated login info, such as email or phone number, and it includes your app's ID. Check the returned ID against your app's ID to make sure the access token is valid for your app.
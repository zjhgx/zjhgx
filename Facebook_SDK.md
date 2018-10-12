## Account Kit
Account Kit �ĵ�¼���̼��ʻ�ע����ʻ���¼Ϊһ�塣�������ʻ��Ƿ��Ѿ����ڣ�Ҳ���贴�����������û�ע�����̡���¼��ע��ɹ���Account Kit ��������Ӧ���ṩ��¼�û�����֤ƾ֤��

### ���ʿ���
An access token returned from the SDK allows you to verify the authenticity of a user's identity on the server side when processing requests for your application.<br>
ͨ���� SDK ���صķ��ʿ���������ڴ���Ӧ������ʱ�ӷ���������֤�û�����ݡ�
 * �ɹ��ĵ�¼�ᴴ��һ���ʻ���ź͹����ķ��ʿ��A successful login creates an Account ID and an associated access token.
* ���ʿ�������ڷ��� Account Kit REST API��The access token can be used to access Account Kit REST APIs.
* ��Ӧ�ý����ʿ������Ӧ�õķ�������������֤�û���ݡ�You should pass the access token to your application's server to verify the user's identity.
It's a good practice to include the access token with every server request to your application and to verify the user ID from the token and not directly from the client. This helps protect your application from unauthorized uses.

##### �û����ʿ���
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
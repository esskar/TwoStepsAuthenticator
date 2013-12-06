TwoStepsAuthenticator
=====================

.net implementation of the TOTP: Time-Based One-Time Password Algorithm and HOTP: HMAC-Based One-Time Password Algorithm<br/>
RFC 6238 http://tools.ietf.org/html/rfc6238<br>
RFC 4226 http://tools.ietf.org/html/rfc4226

Compatible with Microsoft Authenticator for Windows Phone, and Google Authenticator for Android and iPhone.

You can use this library as well for a client application (if you want to create your own authenticator) or for a server application (add two-step authentication on your asp.net website)

For a client application, you need to save the secret key for your user. <br/>
Then, you only have to call the method GetCode(string) :

<pre><code>
var secret = user.secretAuthToken;
var authenticator = new TwoStepsAuthenticator.TimeAuthenticator();
var code = authenticator.GetCode(secret);
</code></pre>

On a server application, you will have to generate a secret key, and share it with the user, who will have to enter it in his own authenticator app.

<pre><code>
var key = TwoStepsAuthenticator.Authenticator.GenerateKey();
</code></pre>

When the user will login, he will have to give you the code generated by his authenticator.<br/>
You can check if the code is correct with the method CheckCode(string secret, string code).<br/>
If the code is incorrect, don't log him.

<pre><code>
var secret = user.secretAuthToken;
var code = Request.Form["code"];
var authenticator = new TwoStepsAuthenticator.TimeAuthenticator();
bool isok = authenticator.CheckCode(secret, code);
</code></pre>

Every time-based code should only be used once. A build in mechanism ensures that. If you want to control this check by your self you can pass in an instance of IUsedCodesManager.

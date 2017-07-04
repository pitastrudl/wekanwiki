E-mail is quite important in WeKan, as without it you can't send password reset links nor can you verify your e-mail address. Here are some ways to figure out what is wrong with your mail server settings in WeKan.

## Log Files
Firstly, make sure you're logged into your server and following your log files.

    @:~$ tail -f path/to/wekan.log

If you're using the Docker container through docker-compose, you can follow the log file like this:

    @:~$ docker-compose logs -f wekan

If you're using a snap package, you'll get the logs with

    @:~$ journalctl -u snap.wekan.wekan

## Error Messages
Once you've got the log files in front of you, go to the WeKan frontend and send a password reset link, or try to register. This will try to send an e-mail, and you should see any error messages in the log file.

### Wrong Port
If you see an error message like the following one, your port number is wrong. If you're using plain old SMTP or STARTTLS, your port should be 25. If you're using TLS, you may need to change your port to 465. Some mail servers may use port 587 instead of the two above.

```
wekan_1      | Exception while invoking method 'forgotPassword' Error: connect ECONNREFUSED 64.22.103.211:587
wekan_1      |     at Object.Future.wait (/build/programs/server/node_modules/fibers/future.js:449:15)
wekan_1      |     at Mail._syncSendMail (packages/meteor.js:213:24)
wekan_1      |     at smtpSend (packages/email.js:110:13)
wekan_1      |     at Object.Email.send (packages/email.js:168:5)
wekan_1      |     at AccountsServer.Accounts.sendResetPasswordEmail (packages/accounts-password/password_server.js:614:9)
wekan_1      |     at [object Object].Meteor.methods.forgotPassword (packages/accounts-password/password_server.js:546:12)
wekan_1      |     at packages/check.js:130:16
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at Object.exports.Match._failIfArgumentsAreNotAllChecked (packages/check.js:129:41)
wekan_1      |     at maybeAuditArgumentChecks (packages/ddp-server/livedata_server.js:1734:18)
wekan_1      |     at packages/ddp-server/livedata_server.js:719:19
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at packages/ddp-server/livedata_server.js:717:40
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at packages/ddp-server/livedata_server.js:715:46
wekan_1      |     at [object Object]._.extend.protocol_handlers.method (packages/ddp-server/livedata_server.js:689:23)
wekan_1      |     - - - - -
wekan_1      |     at Object.exports._errnoException (util.js:907:11)
wekan_1      |     at exports._exceptionWithHostPort (util.js:930:20)
wekan_1      |     at TCPConnectWrap.afterConnect [as oncomplete] (net.js:1081:14)
```

### Wrong Protocol
If you have the "Enable TLS support for SMTP server", but your does not directly support TLS (it may use STARTTLS instead), then you'll get the following error. Just uncheck the checkbox in the Admin Panel.

```
wekan_1      | Exception while invoking method 'forgotPassword' Error: 139872240588608:error:140770FC:SSL routines:SSL23_GET_SERVER_HELLO:unknown protocol:../deps/openssl/openssl/ssl/s23_clnt.c:794:
wekan_1      |     at Object.Future.wait (/build/programs/server/node_modules/fibers/future.js:449:15)
wekan_1      |     at Mail._syncSendMail (packages/meteor.js:213:24)
wekan_1      |     at smtpSend (packages/email.js:110:13)
wekan_1      |     at Object.Email.send (packages/email.js:168:5)
wekan_1      |     at AccountsServer.Accounts.sendResetPasswordEmail (packages/accounts-password/password_server.js:614:9)
wekan_1      |     at [object Object].Meteor.methods.forgotPassword (packages/accounts-password/password_server.js:546:12)
wekan_1      |     at packages/check.js:130:16
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at Object.exports.Match._failIfArgumentsAreNotAllChecked (packages/check.js:129:41)
wekan_1      |     at maybeAuditArgumentChecks (packages/ddp-server/livedata_server.js:1734:18)
wekan_1      |     at packages/ddp-server/livedata_server.js:719:19
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at packages/ddp-server/livedata_server.js:717:40
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at packages/ddp-server/livedata_server.js:715:46
wekan_1      |     at [object Object]._.extend.protocol_handlers.method (packages/ddp-server/livedata_server.js:689:23)
wekan_1      |     - - - - -
wekan_1      | 
wekan_1      |     at Error (native)
```

### Self-signed Certificate
Unfortunately at this stage, WeKan does not support self-signed certificates. You will see the following error if your SMTP server is using a self-signed certificate. The only ways to remedy this are to either get a certificate from a CA, or remove the TLS certificate completely.

```
wekan_1      | Exception while invoking method 'forgotPassword' Error: 139872240588608:error:140770FC:SSL routines:SSL23_GET_SERVER_HELLO:unknown protocol:../deps/openssl/openssl/ssl/s23_clnt.c:794:
wekan_1      |     at Object.Future.wait (/build/programs/server/node_modules/fibers/future.js:449:15)
wekan_1      |     at Mail._syncSendMail (packages/meteor.js:213:24)
wekan_1      |     at smtpSend (packages/email.js:110:13)
wekan_1      |     at Object.Email.send (packages/email.js:168:5)
wekan_1      |     at AccountsServer.Accounts.sendResetPasswordEmail (packages/accounts-password/password_server.js:614:9)
wekan_1      |     at [object Object].Meteor.methods.forgotPassword (packages/accounts-password/password_server.js:546:12)
wekan_1      |     at packages/check.js:130:16
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at Object.exports.Match._failIfArgumentsAreNotAllChecked (packages/check.js:129:41)
wekan_1      |     at maybeAuditArgumentChecks (packages/ddp-server/livedata_server.js:1734:18)
wekan_1      |     at packages/ddp-server/livedata_server.js:719:19
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at packages/ddp-server/livedata_server.js:717:40
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at packages/ddp-server/livedata_server.js:715:46
wekan_1      |     at [object Object]._.extend.protocol_handlers.method (packages/ddp-server/livedata_server.js:689:23)
wekan_1      |     - - - - -
wekan_1      | 
wekan_1      |     at Error (native)
```

### Incorrect TLS Certificate
Lastly, if you see the following error message it is because the certificate has not been correctly installed on the SMTP server.

```
wekan_1      | Exception while invoking method 'forgotPassword' Error: unable to verify the first certificate
wekan_1      |     at Object.Future.wait (/build/programs/server/node_modules/fibers/future.js:449:15)
wekan_1      |     at Mail._syncSendMail (packages/meteor.js:213:24)
wekan_1      |     at smtpSend (packages/email.js:110:13)
wekan_1      |     at Object.Email.send (packages/email.js:168:5)
wekan_1      |     at AccountsServer.Accounts.sendResetPasswordEmail (packages/accounts-password/password_server.js:614:9)
wekan_1      |     at [object Object].Meteor.methods.forgotPassword (packages/accounts-password/password_server.js:546:12)
wekan_1      |     at packages/check.js:130:16
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at Object.exports.Match._failIfArgumentsAreNotAllChecked (packages/check.js:129:41)
wekan_1      |     at maybeAuditArgumentChecks (packages/ddp-server/livedata_server.js:1734:18)
wekan_1      |     at packages/ddp-server/livedata_server.js:719:19
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at packages/ddp-server/livedata_server.js:717:40
wekan_1      |     at [object Object]._.extend.withValue (packages/meteor.js:1122:17)
wekan_1      |     at packages/ddp-server/livedata_server.js:715:46
wekan_1      |     at [object Object]._.extend.protocol_handlers.method (packages/ddp-server/livedata_server.js:689:23)
wekan_1      |     - - - - -
wekan_1      |     at Error (native)
wekan_1      |     at TLSSocket.<anonymous> (_tls_wrap.js:1063:38)
wekan_1      |     at emitNone (events.js:67:13)
wekan_1      |     at TLSSocket.emit (events.js:166:7)
wekan_1      |     at TLSSocket._init.ssl.onclienthello.ssl.oncertcb.TLSSocket._finishInit (_tls_wrap.js:621:8)
wekan_1      |     at TLSWrap.ssl.onclienthello.ssl.oncertcb.ssl.onnewsession.ssl.onhandshakedone (_tls_wrap.js:453:38)
```

## No News Is Good News
Of course, if you don't see any of these errors in your WeKan log file, then the problem is not in WeKan. Check your SMTP server's mail logs (if you can) to get a better idea of what might be going wrong.
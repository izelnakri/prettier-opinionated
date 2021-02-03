- prettier-opinionated/group-variables -> usage order & alphabetical space in between only not when if after
- prettier-opinionated/spaces-between-groups
- prettier-opinionated/group-awaits -> usage order space before/after
- prettier-opinionated/space-before-return
- prettier-opinionated/private-helper-functions-at-bottom

from:

```js
let group = this.server.create('group');
let user = this.server.create('user');
this.server.create('membership', { group, user });
this.server.create('email', { user });
```

to:

```js
let group = this.server.create('group');
let user = this.server.create('user');

this.server.create('membership', { group, user });
this.server.create('email', { user });
```

------------

from:

```js
let group = this.server.create('group');

let user = this.server.create('user');

this.server.create('membership', { group, user });

this.server.create('email', { user });
```

to:

```js
let group = this.server.create('group');
let user = this.server.create('user');

this.server.create('membership', { group, user });
this.server.create('email', { user });
```

------------

from:

```js
this.server.create('email', { user });
assert.equal(invite.recipient.user, null);
let response = await fetch(`${API}/v1/email`, { method: 'POST' });
let responsePayload = await response.json();
assert.ok(response.ok);
assert.matchJson(responsePayload, {
  email: {
    id: email.id,
    address: 'contact@example.com
  },
});
assert.equal(email.user.id, user.id);
```

to:

```js
this.server.create('email', { user });

assert.equal(email.user, null);

let response = await fetch(`${API}/v1/email`, { method: 'POST' });
let responsePayload = await response.json();

assert.ok(response.ok);
assert.matchJson(responsePayload, {
  email: {
    id: email.id,
    address: 'contact@example.com
  },
});
assert.equal(email.user.id, user.id);
```

-------------

from:

```js
await visit(`/users/${user.id}/emails`);
assert.equal(currentURL(), `/users/${user.id}/emails`);
await click(`[data-test-user-details="${user.id}"]`);
await select(`[data-test-something]`, something);
assert.dom('[data-test-something]').hasValue(something);
```

to:

```js
await visit(`/users/${user.id}/emails`);

assert.equal(currentURL(), `/users/${user.id}/emails`);

await click(`[data-test-user-details="${user.id}"]`);
await select(`[data-test-something]`, something);

assert.dom('[data-test-something]').hasValue(something);
```

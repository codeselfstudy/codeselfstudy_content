title: How to Generate Gravatar Images with JavaScript/Node
date: 2019-03-09 22:59
category: JavaScript
slug: gravatar-javascript-node
authors: Josh

Someone asked a question at the meetup today on how to create avatars on a site. The fastest method is probably to use Gravatar. Gravatar is a service that displays user profile pictures based on their email addresses. If the user hasn't signed up with Gravatar, a variety of default avatars can be shown.

Here is my Gravatar as an example:

<img src="https://www.gravatar.com/avatar/938bb9e5bb7bfa900901a4e7abce0db7?d=identicon" alt="Josh">

In the simplest form, you load an image that is built with this structure:

```text
https//www.gravatar.com/avatar/<md5sum_of_email_address>
```

Here's a solution that will work in Node.js, and allow you to choose a different type of default image for when an email address doesn't have a Gravatar:

```javascript
const crypto = require('crypto');

function generateAvatarUrl(emailAddress, options = {}) {
    const defaultImage = options.defaultImage || 'identicon';
    const emailHash = crypto.createHash('md5').update(emailAddress).digest('hex');
    return `https://www.gravatar.com/avatar/${emailHash}?d=${defaultImage}`;
}
```

Then you can call the function with an email address to generate an image URL:

```
const avatarUrl = generateAvatarUrl('user@example.com');
```

When an email address doesn't have a gravatar, the function above will use an "identicon" by default, which looks like this:

<img src="https://www.gravatar.com/avatar/b43b6d0ebbe7351b469696004ecbbd18?d=identicon" alt="Identicon">

Or you could run the function like this:

```
const avatarUrl = generateAvatarUrl('not_an_email_account@example.com', { defaultImage: 'monsterid' });
```

to produce a random monster ID image by default:

<img src="https://www.gravatar.com/avatar/b43b6d0ebbe7351b469696004ecbbd18?d=monsterid" alt="Monster ID">

There are more options available in the [documentation](https://en.gravatar.com/site/implement/images/).

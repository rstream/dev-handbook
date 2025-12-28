# AJAX

[← back](index.md)

Old and new syntax of AJAX requests.

## GET

### Old-school GET request

```js
const name = encodeURIComponent("John Doe");
const admin = encodeURIComponent("T");
const xhr = new XMLHttpRequest();
xhr.open('GET', `/get.php?name=${name}&admin=${admin}`, true);
xhr.onload = () => {
	if (xhr.status === 200) {
		console.log('> done', xhr.responseText);
	} else {
		console.error('> fail', xhr.status, xhr.statusText);
	}
};
xhr.onerror = () => {
    console.error('Network error');
}
xhr.send();
```

### Modern GET request

```js
const params = new URLSearchParams({
	name: "John Doe",
	admin: "T"
}).toString();
try {
	const response = await fetch(`/get.php?${params}`);
	if (response.ok) {
		const text = await response.text();
		console.log('> done', text);
	} else {
		console.error('> fail', response.status, response.statusText);
	}
} catch(e) {
	console.error(e);
}
```

## POST

### Old-school POST request

```js
const payload = JSON.stringify({
    name: "John Doe",
    admin: "T"
});
const xhr = new XMLHttpRequest();
xhr.open('POST', '/post.php', true);
xhr.setRequestHeader('Content-Type', 'application/json');
xhr.onload = () => {
	if (xhr.status === 200) {
		const data = JSON.parse(xhr.responseText);
		console.log('> done', data);
	} else {
		console.log('> fail', xhr.status, xhr.statusText);
	}
};
xhr.onerror = () => {
	console.error('Network error');
}
xhr.send(payload);
```

### Modern POST request

```js
const payload = JSON.stringify({
    name: "John Doe",
    admin: "T"
});
try {
	const response = await fetch('/post.php', {
		method: 'POST',
		headers: {
			'Content-Type': 'application/json'
		},
		body: payload
	});
	if (response.ok) {
		const data = await response.json();
		console.log('> done', data);
	} else {
		console.log('> fail', response.status, response.statusText);
	}
} catch(e) {
	console.error('Network error', e);
}
```
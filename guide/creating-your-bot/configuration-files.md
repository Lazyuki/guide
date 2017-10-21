## Configuration files

As you get deeper into development, you may need to interact with sensitive data or data that gets used in multiple locations, such as:

* Database passwords
* API keys
* Command prefix(es)
* A list of bot owner IDs

Having that kind of data hard-coded in each of your files can be a bit bothersome and is less than ideal, to say the least. This is where configuration files come in - they're great for storing static data that can be easily updated in a single place.

### Implementing your config file

Go to your code editor and make a new file. Add in the code below and save it as `config.json`, in the same directory as your main bot file.

```json
{
	"prefix": "!",
	"token": "your-token-goes-here"
}
```

Go back to your main bot file, locate the `const client = new Discord.Client()` line, and add this above it:

```js
const config = require('./config.json');
```

Next, copy your token from the `client.login('your-token-goes-here')` line and paste into the `config.json` file. Make sure to keep it between the double quotes.

Now you can simply do `client.login(config.token)` to login! If you want to use a different prefix than `!`, you can change that as well.

### Storing additional data

As previously mentioned, you'll probably want to store more than just your token and prefix at one point or another. If you want to store more data, just add another key/value pair to the list!

```json
{
	"prefix": "!",
	"token": "your-token-goes-here",
	"meaning_of_life": 42,
	"passwords_array": ["please", "dont", "hack", "me"],
	"secret_passcodes": {
		"bank": 1234,
		"home": 4321
	}
}
```

#### Storing only arrays

In the above example, you can see that you can store different types of data (strings, numbers, arrays, and objects). But what about when you only need an array of data? For example, you might want to pick a random response from an array of responses. You might be thinking of just doing something like this:

```js
// random-responses.json
{
	"responses": ["Hi!", "Hey!", "What's up?", "How are you?"]
}

// index.js
const responseArray = require('./random-responses.json').responses;
console.log(responseArray); // ["Hi!", "Hey!", "What's up?", "How are you?"]
```

But instead of doing that, you can make your entire JSON file an array!

```js
// random-responses.json
[
	"Hi!", "Hey!", "What's up?", "How are you?"
]

// index.js
const responseArray = require('./random-responses.json');
console.log(responseArray); // ["Hi!", "Hey!", "What's up?", "How are you?"]
```

This makes our code a bit more clean and easy to understand.
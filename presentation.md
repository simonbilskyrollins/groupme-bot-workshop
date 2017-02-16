% How to make a GroupMe bot
% (and other selected topics in app development/deployment)
% Simon Bilsky-Rollins


# Outline

* What is a bot?
* What do you need to make a bot?
* The story of Beep Boop
* Deployment
* Testing


# What is a bot?

* A computer that engages in conversation with a human
* Examples: Siri, Alexa, Cortana, Google
* Here: memes and canned jokes = conversation


# What do you need to make a bot?

* Medium for human-computer interaction
* A computer connected to this medium
* A program to tell the computer how to participate in the conversation


# The story of Beep Boop

* Step 1: Get a key from GroupMe
	* Go to the [GroupMe API portal](https://dev.groupme.com)

* Step 2: Hello world
	* `test.json`
		```json
		{
		  "bot_id"  : "j5abcdefg",
		  "text"    : "Hello world",
		  "attachments" : [
		    {
		      "type"  : "image",
		      "url"   : "https://i.groupme.com/somethingsomething.large"
		    }
		  ]
		}
		```

	*	```bash
		curl -X POST -d @test.json -H 'Content-Type: application/json' https://api.groupme.com/v3/bots/post
		```

* Step 3: Implement a **callback server**
	* [Starter Node.js code from GroupMe](https://github.com/groupme/bot-tutorial-nodejs)


# The story of Beep Boop (cont.)

* Step 4: Define what the server responds to
	* Regex! For example, to match a message that mentions the word "meme" or "memes":
		```javascript
		var memeRegex = /\bmemes?\b/i
		```
	  	![](https://imgs.xkcd.com/comics/regular_expressions.png)


# The story of Beep Boop (cont.)

* Step 5: Tell the bot what to say in response
	```javascript
	if (message.text.match(memeRegex)) {
	  var botResponse = 'I hope this brightens your day'
	  postMessage(botResponse)
	}
	```


# The story of Beep Boop (cont.)

* Step 6: Setup your project environment
	```bash
	nano .env
	npm install
	```

* Step 7: Test it out!
	```bash
	npm start
	open http://localhost:5000
	curl -H "Accept: application/json" -H "Content-Type: application/json" \
		-d @test.json http://localhost:5000
	```


# The story of Beep Boop (cont.)

* Step 8: Let's get some memes
	* Annoying: GroupMe requires images to be uploaded to their own image service.
	* Less annoying: someone already made an npm package to handle (some of) that for us.
	* Barely annoying at all: someone has also made an npm package that wraps the Reddit API.

* Step 9: Beep Boop remembers
	* Group members ask Beep Boop to call them by a certain nickname.
	* Postgres database to remember nicknames.


# Deployment

* We need to deploy our app to some publicly-available server for two main reasons:
	* GroupMe needs somewhere to send messages to.
	* Your laptop isn't always on.

* Heroku!
	* Free hosting
	* Free database
	* Easy deployment (integrated with GitHub)


# Deployment (cont.)

* A few preparations before we deploy:
	* Need to specify Node.js and NPM versions in `package.json`.
	* Need to configure environment variables on the server.


# Testing

* Boring!
* Actually kind of important though
* Plus, lots of nice tools that make testing easier
	* Libraries for syntax checking
	* Libraries for unit testing
	* Travis for continuous integration


# Thank You!

Questions?

% How to make a GroupMe bot
% (and other selected topics in app development/deployment)
% Simon Bilsky-Rollins


# Outline

* What is a bot?
* What do you need to make a bot?
* The story of Beep Boop
* Testing
* Deployment


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

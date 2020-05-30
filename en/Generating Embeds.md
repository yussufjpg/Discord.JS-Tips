# Generating Embeds
To generate embeds without long repeated codes we can make it a function and generate embeds as we like.

**Making the Function**
```js
// You need (title,desc,footerText,thumb) 
// so that you can change embed as you need.
function  generateEmbed(title,desc,footerText,thumb){ // You can also declare variable types to prevent some errors.
	return {embed:{
		color: 15844367, // Color of the straight line on the left
		title:`${title}`, // Title of embed
		description:`${desc}`, // Description
		timestamp: new  Date(), // Timestamp
		thumbnail:{
			url:thumb // Picture on the right top
		},
		footer: {
			icon_url: client.user.avatarURL, // Bottom left icon you can put a variable in here
			text: `${footerText}` // Bottom text
		}
	}};
}
```

**Usage**
```js
// All in one place
message.channel.send(generateEmbed('Just a title','Description comes here!','Bottom text is right here', msg.author.avatarURL))
```
*or*
```js
// This is way more readable.
var title = 'Just a title';
var description = 'Description comes here!';
var footer = 'Bottom text is right here';
var thumbnail = msg.author.avatarURL;
message.channel.send(generateEmbed(title,description,footer,thumbnail))
```
Result you'll get from both of these codes are going to be something like this based on your improvements and changes:

![result is this](https://i.hizliresim.com/81OBGo.png)

Of course you can make this way more sophisticated but this works just fine for me.

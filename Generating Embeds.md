# Embed Generation
```js
function  generateEmbed(title,desc,footerText,thumb){
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
Result you'll get from this code is going to be like something like this based on your improvements and changes:

![result is this](https://i.hizliresim.com/81OBGo.png)

Of course you can make this way more sophisticated but this works just fine for me.

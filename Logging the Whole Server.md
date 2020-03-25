# Logging the Whole Server

Every event is being logged in a channel which is named as value of logChannel variable. 

**Logging voice Channel Activities**

```js
//First we have to write a function to detect users voice activity.

function getUsersVoiceActivity(oldState,newState){
	if(newState.voiceChannel == undefined){
		//If voiceChannel of newState equals to undefined this means user left the channel.
		return var restofLog = `left a voice channel ${oldState.voiceChannel}`;
	}else if(newState.voiceChannel != undefined && oldState.voiceChannel == undefined){
		//If users old voiceChannel equals to undefined and new voiceChannel doesn't, this means user joins a voice channel.
		return var restofLog = `joined a voice channel (${newState.voiceChannel}).`;
	}else if(newState.deaf == true && oldState.deaf == false){
		//If deaf property of oldState equals to false and newState doesn't, this means user deafens himself.
		return var restofLog = 'deafed himself.';
	}else if(newState.deaf == false && oldState.deaf == true){
		//Opposite of detecting deafening.
		return var restofLog = 'stopped deafening himself.';
	}else if(newState.mute == true && oldState.mute == false){
		//If mute property of oldState equals to false and newState doesn't, this means user mutes himself.
		return var restofLog = 'muted himself.';
	}else if(newState.mute == false && oldState.mute == true){
		//Opposite of detecting self mute.
		return var restofLog = 'stopped mutening himself.';
	}else if(newState.voiceChannel != oldState.voiceChannel && oldState.voiceChannel != undefined){
		//If users old and new voiceChannel doesn't equals to undefined this means user switched from old voiceChannel to new voiceChannel.
		return var restofLog = `switched voice channel(${oldState.voiceChannel} to ${newState.voiceChannel}).`;
	}
}

client.on('voiceStateUpdate', (oldState,newState) => {
	let user = client.users.get(newState.id)
	newState.guild.channels.find(channel => channel.name === logChannel).send(`${user.username}#${user.discriminator} ${getUsersVoiceActivity(oldState,newState)}`)
});
```

**Logging New Messages**

```js
client.on('message', message => {
	message.guild.channels.find(channel => channel.name === logChannel).send(`message.author just sent a new message ${message.content} to #${message.channel.name} channel.`)
})
```

**Logging Message Updates**

```js
client.on('messageUpdate', (oldMessage,newMessage) => {
	oldMessage.guild.channels.find(channel => channel.name === logChannel).send(`${message.author} changed his ${oldMessage.content} message with ${newMessage.content} in ${newMessage.channel.name}.`)
});
```

**Logging Deleted Messages**

```js
client.on(`messageDelete`, message => {
	message.guild.channels.find(channel => channel.name === logChannel).send(`${message.author} deleted his ${message.content} message in ${message.channel.name}.`)
})
```

You can make this look much better with embeds, you can go to 'Generating Embeds' section if you want to make.
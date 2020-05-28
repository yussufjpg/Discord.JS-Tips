# Basic Swear Detection

## First Way

```javascript
const filter =  ['here','comes','the','bad','words'];
if( filter.some(word => message.content.includes(word))  )  {
	message.reply('A sweet notification comes here.');
	message.member.addRole(`role id`).catch(console.error)//Gives a role to message author.
	message.delete(timeout);//Deletes notification message after a little while.
} 
```

## Second Way

You can try this way if the first way doesn't work.

```javascript
var q = 0
const filter = ['here','comes','the','bad','words']
filter.forEach(function(item, q, steamid){
	if(message.content.toLowerCase().includes(kufurler[q])){
		message.reply('A sweet notification comes here.')
		message.member.addRole(`role id`).catch(console.error)//Gives a role to message author.
		message.delete(timeout)//Deletes notification message after a little while.
	}
	q++
});
```


# Basit Küfür Tespiti

**İlk Yol**
```js
const filter =  ['Malum','kelimeler','buraya']
if( filter.some(word => message.content.includes(word))  )  {
	message.reply('A sweet notification comes here.');
	message.member.addRole(`role id`).catch(console.error)//Mesaj sahibine bir rol verir
	message.delete(timeout);//Durumu bildiren mesajı bir süre sonra siler(saniye)
}
```

**İkinci Yol**

İlk yöntem çalışmazsa bu yöntemi deneyebilirsiniz.
```js
var q = 0
const filter = ['Malum','kelimeler','buraya']
filter.forEach(function(item, q, steamid){
	if(message.content.toLowerCase().includes(kufurler[q])){
		message.reply('A sweet notification comes here.')
		message.member.addRole(`role id`).catch(console.error)//Mesaj sahibine bir rol verir
		message.delete(timeout)//Durumu bildiren mesajı bir süre sonra siler(saniye)
	}
	q++
});
```

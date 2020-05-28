# Basit Küfür Tespiti

## İlk Yol

```javascript
const filter =  ['Malum','kelimeler','buraya']
if( filter.some(word => message.content.includes(word))  )  {
    message.reply('Güzel bir bildirim.');
    message.member.addRole(`Rol Id`).catch(console.error)//Mesaj sahibine bir rol verir
    message.delete(timeout);//Durumu bildiren mesajı bir süre sonra siler(saniye)
}
```

## İkinci Yol

İlk yöntem çalışmazsa bu yöntemi deneyebilirsiniz.

```javascript
var q = 0
const filter = ['Malum','kelimeler','buraya']
filter.forEach(function(item, q, steamid){
    if(message.content.toLowerCase().includes(kufurler[q])){
        message.reply('Güzel bir bildirim.')
        message.member.addRole(`Rol Id`).catch(console.error)//Mesaj sahibine bir rol verir
        message.delete(timeout)//Durumu bildiren mesajı bir süre sonra siler(saniye)
    }
    q++
});
```


# Kullanıcı Bazlı Aktiviteleri Kayıt Altına Alma

Kullanıcı bazlı bütün aktiviteler logChannel isimli değişkenin değerine eşdeğer kanala yollanıyor.

**Sesli Kanal Aktivitelerini Tespit Etmek**
Sesli kanal aktivitelerini tespit etmek için öncelikle bir fonksiyon yazıp ['voiceStateUpdate'](https://discord.js.org/#/docs/main/stable/class/Client?scrollTo=e-voiceStateUpdate) eventinden gelen sinyallerle çalışırmalıyız.

```js
//Ses aktivitelerini tespit edebilmek için bir fonksiyon yazmalıyız.

function getUsersVoiceActivity(oldState,newState){
	if(newState.voiceChannel == undefined){
		//Eğer kullanıcının yeni sesli kanalı tanımsız(undefined) ise kullanıcı kanaldan ayrılmıştır.
		return var restofLog = `**${oldState.voiceChannel}** kanalından ayrıldı.`
	}else if(newState.voiceChannel != undefined && oldState.voiceChannel == undefined){
		//Eğer kullanıcının eski sesli kanalı tanımsız(undefined); yeni sesli kanalı tanımsız değilse kullanıcı bir kanala katılmıştır.
		return var restofLog = `**${newState.voiceChannel}** kanalına katıldı.`
	}else if(newState.deaf == true && oldState.deaf == false){
		// Eğer kullanıcının eski aktivitesinde kulaklık(deaf) niteliği(property) false; yeni aktivitesinde true ise kullanıcı kendisini susturmuştur.
		return var restofLog = `**${newState.voiceChannel}** kanalında kulaklığını kapattı.`
	}else if(newState.deaf == false && oldState.deaf == true){
		// Kulaklığı kapatmayı algılamanın tersi.
		return var restofLog = `**${newState.voiceChannel}** kanalında kulaklığını açtı.`
	}else if(newState.mute == true && oldState.mute == false){
		// Eğer kullanıcının eski aktivitesinde susturma(mute) niteliği(property) false; yeni aktivitesinde true ise kullanıcı kendisini susturmuştur.
		return var restofLog = `**${newState.voiceChannel}** kanalında kendisini susturdu.`
	}else if(newState.mute == false && oldState.mute == true){
		// Kendi kendini susturmayı algılamanın tersi.
		return var restofLog = `**${newState.voiceChannel}** kanalında kendi susturmasını kaldırdı.`
	}else if(newState.voiceChannel != oldState.voiceChannel && oldState.voiceChannel != undefined){
		// Eğer kullanıcının eski ve yeni sesli kanalları birbiri ile eşleşmiyorsa kullanıcı başka bir kanala geçmiştir.
		return var restofLog = `**${oldState.voiceChannel}** kanalından ayrılarak **${newState.voiceChannel}** kanalına katıldı.`
	}
}

// Bir ses aktivitesi gerçekleşirse ne olduğunu algılamak için yazdığımız fonksiyonu kullanmalıyız.
client.on('voiceStateUpdate', (oldState,newState) => {
	let user = client.users.get(newState.id)
	newState.guild.channels.find(channel => channel.name === logChannel).send(`${user.username}#${user.discriminator} ${getUsersVoiceActivity(oldState,newState)}`)
});
```

**Yeni Mesajları Kaydetmek**

['message'](https://discord.js.org/#/docs/main/stable/class/Client?scrollTo=e-message) eventi yeni mesaj yollandıkça çalışır.

```js
client.on('message', message => {
	message.guild.channels.find(channel => channel.name === logChannel).send(`${message.author} kullanıcısı  #${message.channel.name} kanalına ${message.content} şeklinde bir mesaj gönderdi.`)
})
```

**Mesaj Güncellemelerini Kaydetmek**

['messageUpdate'](https://discord.js.org/#/docs/main/stable/class/Client?scrollTo=e-messageUpdate) eventi mesajlar güncellendikçe çalışır.

```js
client.on('messageUpdate', (oldMessage,newMessage) => {
	oldMessage.guild.channels.find(channel => channel.name === logChannel).send(`${message.author} kullanıcısı ${newMessage.channel.name} kanalındaki ${oldMessage.content} mesajını ${newMessage.content} şeklinde güncelledi.`)
});
```

**Silinen Mesajları Kaydetmek**

['mesageDelete'](https://discord.js.org/#/docs/main/stable/class/Client?scrollTo=e-messageDelete) eventi bir mesaj silinince çalışır.

```js
client.on(`messageDelete`, message => {
	message.guild.channels.find(channel => channel.name === logChannel).send(`${message.author} kullanıcısının ${message.channel.name} kanalındaki ${message.content} mesajı silindi.`)
})
```

Bu kayıtları embedler ile çok daha gösterişli yapabilirsiniz, bunun için ['Otomatik Embed Oluşturma'](https://github.com/yussufjpg/DiscordJS-Tips/blob/master/tr/Otomatik%20Embed%20Olu%C5%9Fturma.md) isimli bölüme gitmelisiniz.

dipnot: Mesaj tepkilerini de kayıt altına alabilirsiniz ancak bu pek de kayda değer olmadığı için eklemedim.

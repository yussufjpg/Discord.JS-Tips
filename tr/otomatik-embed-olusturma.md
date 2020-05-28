# Otomatik Embed Oluşturma

Uzun, tekrarlanan kodlardan kaçınmak ve istediğimiz şekilde embed oluşturmak için bunu bir fonksiyon haline getirmeliyiz.

**Fonksiyonu Oluşturmak**

```javascript
// İstediğiniz değişiklikleri yapabilmek için,
// (title,desc,footerText,thumb)'a ihtiyacınız olacak
function  generateEmbed(title,desc,footerText,thumb){ // Bazı olası hataları önlemek için değişken tiplerini de tanımlayabilirsiniz.
    return {embed:{
        color: 15844367, // Mesajın solundaki düz çizginin rengi 
        title:`${title}`, // Embed Başlığı
        description:`${desc}`, // Açıklaması
        timestamp: new  Date(), // Zaman Damgası(timestamp)
        thumbnail:{
            url:thumb // Sağ üstteki küçük resim(thumbnail)
        },
        footer: {
            icon_url: client.user.avatarURL, // Sol alttaki ikon bölümü (buraya da bir değişken koyabilirsiniz)
            text: `${footerText}` // En alt kısımdaki yazı (ikonun sağı)
        }
    }};
}
```

**Kullanımı**

```javascript
// Hepsi bir arada
message.channel.send(generateEmbed('Sadece bir Başlık','Açıklama Buraya!','En alttaki yazı tam burada!', msg.author.avatarURL))
```

_şeklinde ya da_

```javascript
// Ayrı ayrı, çok daha okunabilir formatta.
var title = 'Sadece bir Başlık';
var description = 'Açıklama Buraya!';
var footer = 'En alttaki yazı tam burada!';
var thumbnail = msg.author.avatarURL;
message.channel.send(generateEmbed(title,description,footer,thumbnail))
```

Yaptığınız değişikliklere ve iyileştirmelere bağlı olarak sonuç aşağı yukarı bu şekilde olacaktır:

![sonu&#xE7;!](https://camo.githubusercontent.com/4aaa3c9807dd8a9ba92551b125cc143ed8a3dc65/68747470733a2f2f692e68697a6c69726573696d2e636f6d2f4f61594247742e706e67)

Tabiki de çok daha karmaşık yöntemler geliştirebilirsiniz ancak bu haliyle benim işimi oldukça iyi bir şekilde görüyor.


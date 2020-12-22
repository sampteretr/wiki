---
title: BanEx
description: Ban a player with a reason.
tags: ["administration"]
---

## Açıklama

Bir oyuncu herhangi bir nedenle yasaklama.

| İsim     | Açıklama                  |
| -------- | ---------------------------- |
| Oyuncu ID | Yasaklanacak oyuncu için belirlenmiş ID numarası. |
| Sebep | Oyuncunun yasaklanma nedeni.      |

## Sonuç

Bu işlev herhangi bir değer döndürmüyor.

## Örnek

```c
public OnPlayerCommandText( playerid, cmdtext[] )
{
    if (!strcmp(cmdtext, "/yasaklabeni", true))
    {
        // Bu komutu kullanan oyuncuyu şu gerekçe ile yasaklar: "İstek"
        BanEx(playerid, "İstek");
        return 1;
    }
}
/* Oyuncunun sunucu ile bağlantısı kesilmeden önce yasaklanma nedenini göstermek için bir zamanlayıcı kullanmanız gerekir.
Zamanlayıcı da şu şekilde yapılır: */

forward BanExPublic(playerid, reason[]);

public BanExPublic(playerid, reason[])
{
    BanEx(playerid, reason);
}

stock BanExWithMessage(playerid, color, message[], reason[])
{
    // "Yasaklanma Nedeni" yerine oyuncunun ekranında görünmesi istenen mesajın yazılması gerekiyor.
    SendClientMessage(playerid, color, "Yasaklanma Nedeni");
    SetTimerEx("BanExPublic", 1000, false, "ds", playerid, reason);
}

/* Oyuncuyu yasaklamadan önce mesaj göndermek için gerekli işlemleri tamamladıktan sonra yapılması gerekenleri
örnek bir komutla inceleyelim. */

public OnPlayerCommandText(playerid, cmdtext[])
{
    if (strcmp(cmdtext, "/yasaklabeni", true) == 0)
    {
        // Bu komutu kullanan kişinin ekranına "Yasaklandın!" mesajı çıkar, oyuncunun yasaklanma defteri yasak defterine "İstek" olarak kaydedilir.
        BanExWithMessage(playerid, 0xFF0000FF, "Yasaklandın!", "İstek");
        return 1;
    }
    return 0;
}
```

## Related Functions

- [Ban](Ban): Bir oyuncunun sunucudan yasaklanmasını sağlar.
- [Kick](Kick): Bir oyuncunun sunucudan atılmasını sağlar. Ban fonksiyonundan farkı, oyuncunun yeniden giriş yapabilmesidir.

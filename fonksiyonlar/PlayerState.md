| Fonksiyon Adı   |     Parametreler        |                          İşlev                               |
|-----------------|-------------------------|--------------------------------------------------------------|
| PlayerState     |          id             | Oyuncunun güncel durumunu string olarak çekmeye yarar.      |

### **Fonksiyon**

```c
PlayerState(id) 
{
    new pstate[124];
    switch(id)
    {
        case 0: pstate = "Boş";
        case 1: pstate = "Ayakta";
        case 2: pstate = "Sürücü";
        case 3: pstate = "Yolcu";
        case 7: pstate = "Ölü";
        case 8: pstate = "Spawned";
        case 9: pstate = "Spectate";
    }
    return pstate;
}
```

### **Kullanım**

```c

PlayerState(GetPlayerState(playerid));

```

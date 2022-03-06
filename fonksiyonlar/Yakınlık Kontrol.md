| Fonksiyon Adı   |           Parametreler           |                          İşlev                               |
|-----------------|----------------------------------|--------------------------------------------------------------|
| YakinlikKontrol | playerid, targetid, Float:radius | Oyuncunun hedef oyuncu ile arasındaki mesafeyi kontrol eder. |

### **Fonksiyon**

```c
YakinlikKontrol(playerid, targetid, Float:radius)
{
    static
        Float:fX,
        Float:fY,
        Float:fZ;

    GetPlayerPos(targetid, fX, fY, fZ);

    return (GetPlayerInterior(playerid) == GetPlayerInterior(targetid) && GetPlayerVirtualWorld(playerid) == GetPlayerVirtualWorld(targetid)) && IsPlayerInRangeOfPoint(playerid, radius, fX, fY, fZ);
}
```

### **Kullanım**

```c
if(!YakinlikKontrol(playerid, targetid, 5.0)) 
            return SendClientMessage(playerid, -1, "Hedef ID'ye yakın değilsin.");

```

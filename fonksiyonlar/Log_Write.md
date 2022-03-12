| Fonksiyon Adı | Parametreler |                                           İşlev                               |
|---------------|--------------                         |------------------------------------------------------|
| Log_Write     | const path[], const str[], {float,_ } | Belirlediğiniz dosya klasörüne log yazdırmaya yarar. |

### **Fonksiyon**

```c
Log_Write(const path[], const str[], {Float,_}:...)
{
	static
	    args,
	    start,
	    end,
	    File:file,
	    string[1024]
	;
	if((start = strfind(path, "/")) != -1) {
	    strmid(string, path, 0, start + 1);
	    if(!fexist(string))
	        return printf("** Warning: Directory \"%s\" doesn't exist.", string);
	}
	#emit LOAD.S.pri 8
	#emit STOR.pri args
	file = fopen(path, io_append);
	if(!file)
	    return 0;
	if(args > 8)
	{
		#emit ADDR.pri str
		#emit STOR.pri start
	    for (end = start + (args - 8); end > start; end -= 4)
		{
	        #emit LREF.pri end
	        #emit PUSH.pri
		}
		#emit PUSH.S str
		#emit PUSH.C 1024
		#emit PUSH.C string
		#emit PUSH.C args
		#emit SYSREQ.C format
		fwrite(file, string);
		fwrite(file, "\r\n");
		fclose(file);
		#emit LCTRL 5
		#emit SCTRL 4
		#emit RETN
	}
	fwrite(file, str);
	fwrite(file, "\r\n");
	fclose(file);
	return 1;
}

//Hata almamanız için eklemeniz gereken "Oyuncu ismini çekme" fonksiyonu.
IsimCek(playerid)
{
    new isim[MAX_PLAYER_NAME + 1];
    GetPlayerName(playerid, isim, sizeof(isim));
    return isim;
}

```

### **Kullanım**

```c
//Scriptfiles'da logs dosya klasörünün içinde bulunan komut_log.txt adlı dosyaya logu yazdırıyoruz.
public OnPlayerCommandPerformed(playerid, cmd[], params[], result, flags)
{
    Log_Write("logs/komut_log.txt", "%s komut kullandi. > %s", IsimCek(playerid), cmd);
    return 1;
}
```

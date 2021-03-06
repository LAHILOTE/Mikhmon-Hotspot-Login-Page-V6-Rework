## Persiapan Instalasi

#### Setting NTP Server di SNTP Client MikroTik

```
System -> SNTP Client
```

<h6> List NTP Server </h6>
<ul>
  <li>id.pool.ntp.org</li>
  <li>time.google.com</li>
 </ul>

![Seting NTP Server](https://laksa19.github.io/img/sntp-client.jpg)

<h4> Membuat login Member menjadi default </h4>
Edit file login.html di baris 14 menjadi 

```
<body onload="member();">
```

<h4> Input otomatis huruf kecil (auto lowercase) mode voucher dan member </h4>
Edit file login.html mulai baris 120 -> 148

```
// set password = username
function setpass(){
  var user = username.value		
  password.value = user;
}
username.onkeyup = setpass; 
// change to voucher mode
function voucher(){
  username.focus();
  username.onkeyup = setpass;
  username.placeholder = "Kode Voucher";
  username.style = "border-radius:3px;"
  password.type = "hidden";
  infologin.innerHTML  = "Masukkan Kode Voucher kemudian klik login.";
}
// change to member mode
function member(){
  username.focus();
  username.onkeyup = "";
  username.placeholder = "Username";
  username.style = "border-radius:3px 3px 0px 0px;"
  password.type = "password";	
  infologin.innerHTML  = "Masukkan Username dan Password kemudian klik login.";
}
//-->


```

menjadi

```
//set lowercase
function setlower(){
var cekMode = password.type;
if (cekMode === "hidden"){
  var user = username.value 
  user = user.toLowerCase();
  username.value = user;  
  password.value = user;
} else if (cekMode === "password"){
  var user = username.value 
  user = user.toLowerCase();
  username.value = user;
} 
}

username.onkeyup = setlower;

// change to voucher mode
function voucher(){
  username.focus();
  username.placeholder = "Kode Voucher";
  username.style = "border-radius:3px;"
  password.type = "hidden";
  password.value = username.value;
  infologin.innerHTML  = "Masukkan Kode Voucher kemudian klik login.";
}

// change to member mode
function member(){
  username.focus();
  username.placeholder = "Username";
  username.style = "border-radius:3px 3px 0px 0px;"
  password.type= "password";
  password.value = "";
  infologin.innerHTML  = "Masukkan Username dan Password kemudian klik login.";
}
//-->

```

<h4> Fitur QR Code Scanner </h4>

Untuk menggunakan fitur QR CODE SCANNER Anda perlu menambahkan script berikut di MikroTik via Terminal.

```
/ip hotspot walled-garden ip

add action=accept comment="Mikhmon QR Code Scanner" disabled=no dst-host=laksa19.github.io

```

Centang HTTP PAP di hotspot server profile.
![Seting QR Code](https://laksa19.github.io/img/myqr-http-pap.png)

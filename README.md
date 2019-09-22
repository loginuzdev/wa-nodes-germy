# WaNodes Endpoints Documentation

Dokumentasi atas pekerjaankuhh~

## Getting Started

Upload ke VPS dan extract file zip, masuk ke directory lalu edit IP whitelist pada file functions.js
```
const ipWhiteLists = [
    "127.0.0.1",
    //tambahin IP shared hostingmu
];
```

### Prerequisites

Membutuhkan package puppeteer.
Jika tidak bisa akses root pada VPS saya tidak tahu cara install nya jika di start error silahkan baca [https://github.com/GoogleChrome/puppeteer/blob/master/docs/troubleshooting.md#chrome-headless-doesnt-launch-on-unix]

### Installing

Masuk ke directori extractan yang ada file package.json terus 

```
npm install
```
# API Endpoints

 ## QR Code
 ### URL
 ```
 GET http://localhost/json/getqr/:userid
 ```
 
 ### Parameter 
  + userid
    Parameter userid bertipe string, harus unik karena karena ini semacam session.

 ### Response
 ```
 {"success": false, "qrBuffer": "", "error": "", "action": [""]}
 ```
  + success (boolean)
  
    Sukses atau tidaknya operasi yang dilakukan.
    
  + qrBuffer (string)
  
    Jika request yang dilakukan sukses dan terdapat Qr Code yang harus discan, maka akan berbentuk imagebase64. Jika failed atau user sudah login maka akan bernilai ```null```.
    
  + error (string)
  
    Jika request yang dilakukan terdapat error maka variabel ini akan terisi dengan pesan error. Jika sebaliknya maka bernilai ```null``.
    
  + action (array of string)
  
    Log dari proses yang dilakukan.


 ## Screenshoot
 ### URL
 ```
 GET http://localhost/json/ss/:userid
 ```
 
 ### Parameter 
  + userid
    Parameter userid adalah session dari request sebelumnya (QRCode)
 ### Response
 ```
 {"success": false, "screenshoot": ""}
 ```
  + success (boolean)
  
    Sukses atau tidaknya operasi yang dilakukan.
    
  + screenshoot (string)
  
    Jika request yang dilakukan sukses dan terdapat session dengan nama yang ada pada userid maka akan terisi dengan hasil screenshot yang dilakukan dengan imagebase64. Jika sebaliknya maka akan bernilai ```null```.

 ## Send Broadcast
 ### URL
 ```
 POST http://localhost/json/sendbulk/:userid
 ```
 
 ### Parameter 
  + userid
    Parameter userid adalah session dari request sebelumnya (QRCode)
    
### Parameter Body
  ```
  {"message":"Your Message Here!","penerima":["6285xxxxxxx","6281xxxxxx","6289xxxxxxx"],"mime":{"fileName": "gambar.jpg", "data": "buffer_base64"}}
  ```
  
  + message (string)
    
    Pesan yang akan dikirim.
  
  + penerima (array of string)
    
    Penerima yang akan dikirimkan pesan, bertipe array. Kode negara harus ikut, semisal indonesia adalah 62, maka 62856464996.
  
  + mime (object)
    
    Jika pesan yang dikirim tidak disertakan gambar, maka diisi dengan nilai ```null```. Jika tidak maka harus terdapat dua properti yaitu ```fileName``` dan ```data```.
    
    Contoh
    ```"mime":{"filename": "apple-logo.png", "data": "data:image/png;base64,data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQgAAAEICAYAAACj9mr .... "}```
  
 ### Response
 ```
 {"success": true, "message": "Your messages here!", "result": true}
 ```
  + success (boolean)
  
    Sukses atau tidaknya operasi yang dilakukan.
    
  + message (string)
  
    Message yang dikirimkan
    
  + result (boolean, object)
  
    Gak tau apa, tapi kalo sukses true, kadang juga object
    
 ## Destroy Session
 ### URL
 ```
 GET http://localhost/json/destroy/:userid
 ```
 
 ### Parameter 
  + userid
    Parameter userid adalah session yang akan didestroy. Biasanya di lakukan pada saat user logout, biar gak berat bos VPS nya~
 ### Response
 ```
 {"success": true, "msg": ""}
 ```
  + success (boolean)
  
    Sukses atau tidaknya operasi yang dilakukan. Ini pasti true, biar gak dibrute force!
    
  + msg (string)
  
    Biasanya cuman ```task killed```.
    

 ## Get Session Status
 ### URL
 ```
 GET http://localhost/json/getsession/:userid
 ```
 
 ### Parameter 
  + userid
    Parameter userid adalah session yang akan didapatkan statusnya.
 ### Response
 ```
 {"success": true, "hasActiveSession": true}
 ```
  + success (boolean)
  
    Sukses atau tidaknya operasi yang dilakukan. Ini pasti true, biar gak dibrute force!
    
  + hasActiveSession (boolean)
  
    Jika true maka terdapat session aktif, tapi gak tau udah login apa belum. Pokoknya terdapat session aktif.
    

 ## Get All Active Sessions (ADMIN DOANG JGN DIKASIH KE USER!)
 ### URL
 ```
 GET http://localhost/json/pool/
 ```

 ### Response
 ```
 {"success": true, "pool": []}
 ```
  + success (boolean)
  
    Sukses atau tidaknya operasi yang dilakukan.
    
  + pool (array)
  
    Daftar dari Session yang aktif.
    

# NOTE
```for business inquiries: loginuzdevelopment@hotmail.com```

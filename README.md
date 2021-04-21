## React Fetching data api

Okay teman teman kali ini kita akan belajar bagaimana caranya consume data dari api yang sudah pernah kita buat di sesi EXPRESS SQLITE dengan menggunakan REACT.

Pertama tentunya teman teman harus menjalankan server API di file express-sqlite uyang teman teman miliki.

```bash
cd express-sqlite
code .
npm run dev
```

Silakan buka **DBEAVER** dan teman teman bisa lihat di koneksi yang sebelumnya kita lakukan kita mempunyai sebuah table bernama **users** dan memiliki colums id, email, password dan created_at.

Pastikan server api sudah berjalan di port 8000, silakan test create dan read data users dengan file **test.rest**, apabila semuanya berjalan lancar, baru kita akan mulai code **REACT**

## Instalasi project React

Untuk mempermudah installasi project ini, silakan teman teman clone repository project ini saja, tanpa menginsatallnya lewat npm, npx atau yarn.

Buka terminal baru dan jalankan syntax ini di terminal.

```bash
git clone https://github.com/jemblonganvalley/batch8_pagi_react_fetch.git
cd batch8_pagi_react_fetch
yarn install
rm -rf .git
```

> syntax **yarn install** di jalankan Karena teman teman CLone dari sebuah repository git, teaman teman harus melakukan install environtment package yang tertera pada package.json.
> Tanpa melakukan ini, react teman tidak akan berjalan.

## Edit file app.js

Okay, yang pertama tama teman2 harus lakukan adalah mengedit file bernama App.js yang ada dalam folder src menjadi **App.jsx**

> JSX atau javascript extended adalah sebuah penambahan pada pemograman javascript yang memungkinkan kita bisa insert XML code langsung di dalam sintax javascript.

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/m2165c0w6zqcvgpsbljb.gif)

**Jangan lupa pada bagian atas code selalu tambahkan :**
```javascript
import React from 'react'
```

*di gif saya lupa menambahkan*

## React Hook State 
State adalah data private sebuah component. Data ini hanya tersedia untuk component tersebut dan tidak bisa di akses dari component lain. Component dapat merubah statenya sendiri.
[source](https://medium.com/coderupa/react-prop-state-apa-bedanya-7ee61df8257f)

Code state berada di dalam functional atau class component, karena kita tau **JVALLEY** menggunakan functional component, maka kita akan coba meletakan code hook useState pada component app kita.
<small>./src/App.jsx</small>
![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0xe13o69hhcvx8s4uisj.gif)

Bisa teman teamn lihat di gif diatas, saya membuat sebuah Hook use state, dengan array literal
```javascript
const [data, setData] = React.useState([])
```
ada dua variable yang langsung saya buat didalam array, (array litteral), variable pertama bernama **data** merupakan variable penyimpan data state, dan variable kedua bernama **setData** merupakan sebuah function untuk merubah data pada variable pertama (data). Dan kita langsung mendeklarasikan isi dari state tersebut berupa array kosong.

> Biasanya developer menulis state dengan function dispatch / function pengubah nilai state dengan urutan yang serupa, misal [siswa, setSiswa], [absen, setAbsen], [login, setLogin], dan seterusnya..
> > Pengisian array kosong pada default value state di gunakan untuk menghindari error saat proses mapping data dari api, karena map hanya bisa berlaku pada tipe data state.

## React Hook useEffect
useEffect merupakan sebuah component life cycle pada react, metode ini untuk menjalankan code sebelum data view ter render, biasanya digunakan juga untuk menggambil data dari API.

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t288tlj0xmuguhoq7e5d.gif)

Silakan check gif diatas, saya membuat sebuah react hook useState, useState method membutuhkan 2 parameter, parameter pertama merupakan callback function dan parameter kedua merupakan array.

- Callback function dalam useState akan berisi perintah2 yang akan di jalankan sebelum component ter Render.
- Array pada useState berguna sebagai triger effect. nanti kita akan pelajari lebih lanjut mengenai hal ini, sementara disi sebuah array kosong saja.

*Okay kita lanjut, karena file gif terbatas di 30 second, jadi codenya sedikit2 ya guys..*

Next kita akan masukan code fetching ke dalam useState callback,

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/42qpsafy5p81fgs0wa6g.gif)

**fetch** merupakan sebuah function bawaan javascript yang merupakan fungsi untuk mengambil data dari api. Function ini memiliki setidaknya 2 parameter, parameter pertama adalah **endpoint API** dan parameter kedua adalah **options**.

Setelah mengisi endpoint pada parameter pertama, selanjutnya kita akan isi optionsnya. cekidot..

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/iowkouth5bh9b9lxqik1.gif)

karena fetch merupakan sebuah function promise, maka kita bisa tambahkan fungsi fungsi **then** dan **catch**.

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fv859lyynekydweba3m9.gif)

Pada then yang pertama kita menuliskan code : 
```javascript
.then(res => res.json())
```
artinya adalah setelah data dari API di dapatkan, kita langsung merubahnya menjadi bentuk json.

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7vmhcm9y4qs89wf7du4d.gif)

Oke gif diatas, pada then yang kedua kita melakukan callback , dan langsung mengisi state function **setData** dengan data API yang dialiaskan ke sebuah variable bernama **dataApi**

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/o64e53ocpvu234av2p17.gif)

okay terakhir kita menambahkan sebuah error handling, apabila terjadi error maka kita akan berikan informasi error tadi ke console browser.

## Testing hasil fecthing ke component
Okay sebenarnya kita sudah berhasil mengambil data dari API dan meletakannya ke sebuah state bernama **data**.

Sekarang kita coba check apakah state **data** sudah berisi data dari API, silakan simak gif dibawah ini : 

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/df4pyb6oiqryzfbgdbgh.gif)

Gif di atas kita melakukan concat code javascript ke code component jsx, caranya adalah membungkus code javascript dengan kurung kurawal.
```javascript
 return (
    <div className="App">
      {console.log(data)}
    </div>
  );
```

Sekarang teaman teman tinggal jalankan server reactnya dan buka console log pada browser, seperti gif yang dibawah ini.

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g3c641j3b7fsqox28u71.gif)

> Kenapa ada beberapa ARRAY yang muncul di console browser saya
> > Teman teman pasti ingat bahwa Javascript merupakan sebuah bahasa pemrograman yang sifatnya **NON BLOCKING**, console.log() tetap berjalan sebelum data muncul, dan data yang belum terisi hasil fetch merupakan sebuah array kosong, makanya tampilnya demikian..

Jalankan server react dengan code ```bash yarn start ``` dan silakan buka browser untuk akses console nya.

## Maping State data ke Components
Okay langkah selajutnya, setelah kita memastikan data dari API berhasil kita fetch, kita bisa langsung melakukan *ARRAY MAPPING* agar data bisa kita sajikan dalam bentuk view. perhatikan gif dibawah ini

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bjguczm5cmrub30z1zx8.gif)

Gif diatas kita hide dulu sementara code untuk console log, dengan menekan *CTRL + /* di baris code tersebut. 

Selanjutnya kita menjalankan function mapping dengan cara menempelkan data dengan .map() , function map berisi sebuah parameter berbentuk callback yang kita isi dengan variable alias bernama **e**

Untuk mempelajari lebih dalam mengenai array method, silakan teman teman ke [W3SCHOOL](https://www.w3schools.com/jsref/jsref_map.asp).

Okay next... 😇 
silakan check gif dibawah ini ..

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oiyj9ncdlcariwim21u1.gif)

Gif diatas kita menambahkan pada callback funtion di function mapping sebuah return yang berisi conponent jsx, component jsx yang kita isi selanjutnya kita concat kembali dengan parameter **e**, karena data pada api kita bentuknya object, maka params **e** ini merupakan object juga yang tentunya bisa kita akses propery di dalamnya.. 😎 

Sekarang saatnya kita check pada browser, apakah data benar benar tampil di sana, 

![https://dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dy52119zoko8vl99npfu.gif)

Yeay.. data berhasil muncul ke browser..
But wait.. ada error di console.. 😢

![dev.to](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c0rxmex7taiwi8bhe2ep.png)

Hal ini di karenakan React mewajibkan lopping component diberikan sebuah atribute bernama **key**, yang berisi unique value, nah kita bisa manfaatkan id pada database kita untuk mengisi atribute key ini. silakan check gif dibawah ini 

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uwedp9j9mw0uabuz2lz7.gif)

Nice..🙂
Selamat, teman teman sudah berhasil fetching data dari API di React js.



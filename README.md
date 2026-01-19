<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Aplikasi UMKM Lengkap</title>
<style>
body{font-family:Arial;padding:20px}
input,button{margin:5px;padding:5px}
table{border-collapse:collapse;width:100%;margin-top:10px}
th,td{border:1px solid #333;padding:6px;text-align:center}
h2{background:#2c7be5;color:white;padding:10px}
</style>
</head>
<body>

<h2>Aplikasi UMKM Lengkap</h2>

<h3>Input Produk</h3>
<input id="p_nama" placeholder="Nama Produk">
<input id="p_harga" type="number" placeholder="Harga">
<button onclick="tambahProduk()">Tambah</button>

<table id="tProduk">
<tr><th>Nama</th><th>Harga</th></tr>
</table>

<hr>

<h3>Input Penjualan</h3>
<input id="j_nama" placeholder="Nama Produk">
<input id="j_qty" type="number" placeholder="Qty">
<input id="j_harga" type="number" placeholder="Harga">
<button onclick="tambahPenjualan()">Tambah</button>

<table id="tPenjualan">
<tr><th>Produk</th><th>Qty</th><th>Total</th></tr>
</table>

<hr>

<h3>Input Pengeluaran</h3>
<input id="k_ket" placeholder="Keterangan">
<input id="k_jml" type="number" placeholder="Jumlah">
<button onclick="tambahPengeluaran()">Tambah</button>

<table id="tKeluar">
<tr><th>Keterangan</th><th>Jumlah</th></tr>
</table>

<hr>

<h3>Laporan</h3>
<p>Total Penjualan: Rp <span id="totJual">0</span></p>
<p>Total Pengeluaran: Rp <span id="totKeluar">0</span></p>
<p><b>Laba Bersih: Rp <span id="laba">0</span></b></p>

<script>
let produk=[], penjualan=[], keluar=[];
function simpan(){ 
localStorage.setItem("produk",JSON.stringify(produk));
localStorage.setItem("penjualan",JSON.stringify(penjualan));
localStorage.setItem("keluar",JSON.stringify(keluar));
}
function muat(){
produk=JSON.parse(localStorage.getItem("produk"))||[];
penjualan=JSON.parse(localStorage.getItem("penjualan"))||[];
keluar=JSON.parse(localStorage.getItem("keluar"))||[];
render();
}
function tambahProduk(){
produk.push({nama:p_nama.value,harga:+p_harga.value});
p_nama.value="";p_harga.value="";
simpan();render();
}
function tambahPenjualan(){
let total=j_qty.value*j_harga.value;
penjualan.push({nama:j_nama.value,qty:j_qty.value,total});
j_nama.value="";j_qty.value="";j_harga.value="";
simpan();render();
}
function tambahPengeluaran(){
keluar.push({ket:k_ket.value,jml:+k_jml.value});
k_ket.value="";k_jml.value="";
simpan();render();
}
function render(){
let tp=document.getElementById("tProduk");
tp.innerHTML="<tr><th>Nama</th><th>Harga</th></tr>";
produk.forEach(p=>tp.innerHTML+=`<tr><td>${p.nama}</td><td>${p.harga}</td></tr>`);

let tj=document.getElementById("tPenjualan");
tj.innerHTML="<tr><th>Produk</th><th>Qty</th><th>Total</th></tr>";
let totJ=0;
penjualan.forEach(j=>{tj.innerHTML+=`<tr><td>${j.nama}</td><td>${j.qty}</td><td>${j.total}</td></tr>`; totJ+=j.total;});

let tk=document.getElementById("tKeluar");
tk.innerHTML="<tr><th>Keterangan</th><th>Jumlah</th></tr>";
let totK=0;
keluar.forEach(k=>{tk.innerHTML+=`<tr><td>${k.ket}</td><td>${k.jml}</td></tr>`; totK+=k.jml;});

totJual.innerText=totJ;
totKeluar.innerText=totK;
laba.innerText=totJ-totK;
}
muat();
</script>

</body>
</html>

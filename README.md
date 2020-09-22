  
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="utf-8">
<title>Adam Asmaca Oyunu EMTEK</title>
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
<style>
.harf,.bharf{
width: 50px;
height: 50px;
margin-bottom:4px;
}
 
</style>
</head>
<body>
<div class="container">
<form>
<div class="col-md-6">
<div class="form-group">
<label for="daracagi">Adam Asma Arenası</label>
<textarea id="daracagi" class="form-control" rows="6"></textarea>
</div>
</div>
<div class="col-md-6">
<div class="form-group">
<label for="cikan-harf">Çıkan Harfler</label>
<textarea id="cikan-harf" class="form-control" rows="6"></textarea>
</div>
</div>
<div class="col-md-12">
<div class="form-group">
<label for="cikankelime">Aranan Kelime</label>
</div>
<div class="form-group" id="yertutucu">
</div>
</div>
<div class="col-md-6 col-md-offset-3">
<button type="button" class="btn btn-primary harf">A</button>
<button type="button" class="btn btn-primary harf">B</button>
<button type="button" class="btn btn-primary harf">C</button>
<button type="button" class="btn btn-primary harf">Ç</button>
<button type="button" class="btn btn-primary harf">D</button>
<button type="button" class="btn btn-primary harf">E</button>
<button type="button" class="btn btn-primary harf">F</button>
<button type="button" class="btn btn-primary harf">G</button>
<button type="button" class="btn btn-primary harf">Ğ</button>
<button type="button" class="btn btn-primary harf">H</button>
<button type="button" class="btn btn-primary harf">I</button>
<button type="button" class="btn btn-primary harf">İ</button>
<button type="button" class="btn btn-primary harf">J</button>
<button type="button" class="btn btn-primary harf">K</button>
<button type="button" class="btn btn-primary harf">L</button>
<button type="button" class="btn btn-primary harf">M</button>
<button type="button" class="btn btn-primary harf">N</button>
<button type="button" class="btn btn-primary harf">O</button>
<button type="button" class="btn btn-primary harf">Ö</button>
<button type="button" class="btn btn-primary harf">P</button>
<button type="button" class="btn btn-primary harf">R</button>
<button type="button" class="btn btn-primary harf">S</button>
<button type="button" class="btn btn-primary harf">Ş</button>
<button type="button" class="btn btn-primary harf">T</button>
<button type="button" class="btn btn-primary harf">U</button>
<button type="button" class="btn btn-primary harf">Ü</button>
<button type="button" class="btn btn-primary harf">V</button>
<button type="button" class="btn btn-primary harf">Y</button>
<button type="button" class="btn btn-primary harf">Z</button>
</div>
<div class="col-md-6 col-md-offset-3">
<button type="button" class="btn btn-primary btn-danger btn-block" id="kelime-uret">YENİ KELİME</button>
</div>
</form>
</div>
<script>
var adam = new Array("___\n", " |\n", " O\n", " /", "|", "\\\n", " /", " \\\n", "___");
var kelimeler= ["KAPI","ÇEKMECE","ANAHTARLIK","BİLGİSAYAR","TERZİ","TERAZİ","BİLGİSAYAR","BULMACA","TELEFON","TABLET","DOLAP","GARDOLAP","KUTU","KULAKLIK","SANDALYE","MASA","PRİZ","AVİZE","AMPUL","PENCERE","KABLO","ÇANTA","TERLİK","AĞAÇ","KILIÇ","ÇERÇEVE","AYNA",];
var kelime;
var hak=0;
 
//nesnelerin oluşturulması
var kelimeUret= document.getElementById("kelime-uret");
var daragaci= document.getElementById("daracagi");
var cikanHarf= document.getElementById("cikan-harf");
var harfler= document.querySelectorAll(".harf");
 
//bootstrap(otomatik çalışacak kodlar)
(function(){
harfler.forEach(function(gelen) {
gelen.onclick=function(olay){
 
this.setAttribute("disabled","disabled");
var durum= harfKontrol(kelime,this.textContent);
harfEkle(this.textContent);
if(durum)
{
harfYerlestir(kelime,this.textContent);
 
}
else
{
daragaci.textContent+= adam[hak];
hak++;
}
 
var tireDurum=tireKontrol();
if(!tireDurum)
{
window.alert("TEBRİKLER KAZANDINIZ 👌 EMTEK SİZİ TEBRİK EDER");
tumHarflerPasif();
 
}
if(adam.length<=hak)
{
window.alert("MAALESEF ADAM ASILDI KAYBETTİNİZ");
tumHarfleriYaz(kelime);
tumHarflerPasif();
 
}
}
});
harfSec();
 
})();
 
// olayların atanaması
kelimeUret.onclick=harfSec;
 
//fonksiyonlar
 
function harfSec()
{
var sira=Math.round(Math.random()*kelimeler.length);
kelime=new String(kelimeler[sira]);
kelime=kelime.split("");
 
/*kelime= kelime.map(function(gelen){
return gelen+"_";
});*/
 
yertutucu(kelime);
}
 
//gizli harflerin yerine gösterlicek butonlar
function yertutucu(kelime)
{
var yertutucu=document.getElementById("yertutucu");
yertutucu.innerHTML="";
daragaci.innerHTML="";
tumHarflerAktif();
hak=0;
 
for(var i=0;i<kelime.length;i++)
{
var harf = document.createElement("button");
harf.setAttribute("type","button")
harf.classList.add("btn", "btn-primary", "bharf");
harf.textContent="_";
yertutucu.appendChild(harf);
}
}
 
function harfKontrol(kelime,harf){
return kelime.some(x => x ==harf );
}
 
function harfYerlestir(kelime,harf){
var bharfler= document.querySelectorAll(".bharf");
for(sira in kelime)
{
if(harf==kelime[sira])
{
bharfler[sira].textContent=harf;
}
}
}
 
function tumHarfleriYaz(kelime)
{
var bharfler= document.querySelectorAll(".bharf");
for(sira in kelime)
{
harfYerlestir(kelime,kelime[sira]);
}
}
 
function tumHarflerPasif()
{
harfler.forEach(function(eleman){
eleman.setAttribute("disabled","disabled");
});
 
}
function tumHarflerAktif()
{
harfler.forEach(function(eleman){
eleman.removeAttribute("disabled");
});
 
}
function tireKontrol()
{
var durum= false;
var bharfler= document.querySelectorAll(".bharf");
 
for(sira in bharfler)
{
 
if(bharfler[sira].textContent=="_")
{
durum=true;
}
}
return durum;
 
}
 
function harfEkle(harf)
{
cikanHarf.textContent=cikanHarf.textContent+" "+harf;
}
</script>
</body>
</html>

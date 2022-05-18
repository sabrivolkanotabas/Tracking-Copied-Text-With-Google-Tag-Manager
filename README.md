<h1>Kopyalanan Değeri Takip Etme İşlemi</h1>

<h3>Kopyalanan metni Google Analytics'e "Kopyalanan Metin" ve "Metin Uzunluğu" olarak gönderme</h3>

<ul>
<li> Google Tag Manager üzerinden Custom HTML bir tag oluşturun ve trigger'ını bütün sayfalarda görünecek şekilde ayarlayın </li>
<li> Aşağıda yer alan kodu açtığınız tag içerisine yerleştirin 

    <script>
    document.addEventListener("copy", function (e) {
	  //Kopyalanan text bilgisini tutmak için kullanılır
	  var copiedText = "";

	  //Eğer ki seçilen bir text bilgisi var ise çalışsın
	  if (window.getSelection) {
	    copiedText = window.getSelection().toString();
	  } else if (document.selection && document.selection.type != "Control") {
	    copiedText = document.selection.createRange().text;
	  }

	  //Kopyalanan bir değer boş değilse dataLayer'a event olarak gönderme
	  if (copiedText.trim().length > 0) {
	    window.dataLayer = window.dataLayer || [];
	    window.dataLayer.push({
	      event: "anatomi_text_copied",
	      kopyalananText: copiedText,
	      kopyalananTextUzunlugu: copiedText.length,
	    });
	  } else {
	    return false;
	  }
	});
    </script>
</li>
<li> Gelen verileri Google Analytics'e göndermek için 2 adet variable oluşturun bunlardan biri kopyalanan text değerini almak için "kopyalananText" diğeri ise kopyalanan uzunluk bilgisini elde etmek için "kopyalananTextUzunlugu" şeklinde olmalıdır</li>
<li>Bir trigger custom event trigger oluşturun. Custom Event ise belirlediğiniz event adı olmalıdır. Bu örnek için "anatomi_text_copied" kullanmalıyız.</li>
<li>Verileri Google Analytics'e göndermek için Google Analytics event tag'i oluşturun ve trigger'ını yukarıda ki maddede belirlediğimiz trigger olarak ekleyin. Daha önce tanımladığımız 2 adet variable bilgisini bu event içerisinde gönderecek şekilde ayarlayın</li>
</ul>

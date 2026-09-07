# BULGULAR — dış denetim (2026-09-07)

> Çok-repolu bir öğrenme oturumunda bu site, **kaynağı olan kod deposuyla
> (`heliumnitrate/opicaldistortionlab`) yan yana** denetlendi.
> Siteye hiç dokunulmadı.
>
> **Bir kusur bulundu (kırık iç bağlantı). Sitenin sayısal iddiaları
> ise yeniden üretilerek DOĞRULANDI.**

---

## B1 — Kırık iç bağlantı: `#toolbox`

`distortion-explorer.html:184` gezinme çubuğunda:

```html
<a href="index.html#toolbox">Toolbox</a>
```

Ama `index.html` içinde `id="toolbox"` **yok**. "toolbox" sözcüğü yalnız
gövde metninde geçiyor (satır 674 ve 746), başlık/bölüm kimliği olarak
değil. Sonuç: bağlantıya tıklayan ziyaretçi ilgili bölüme değil,
**index.html'in en başına** düşüyor.

Denetlendi: öteki beş iç bağlantının hepsi sağlam
(`#contact`, `#engine`, `#estimation`, `#freedom`, `#undistortion` ✓).

**Düzeltme.** Toolbox'tan söz eden bölümün sarmalayıcısına `id="toolbox"`
ekle (muhtemelen satır 674 civarındaki bölüm).

---

## DOĞRULANAN — sitenin sayısal iddiası DOĞRU

Sitenin estimation bölümü şunu söylüyor:

> *Ground truth: a strong barrel model, degrees [3, 5, 7, 9, 11]. The
> estimator automatically selects a different, sparser set — degrees
> [2, 3, 4, 5] — and reproduces the radial mapping to an **RMSE of
> 4.0×10⁻⁵ out to the image corner** (five checkerboard boards spanning
> the full field).*

Bu iddia **şüpheyle karşılandı**, çünkü makale (`paper_draft_v7.md` §IX.B)
farklı sayılar veriyor: derece `[2, 3, 4]`, GT'ye karşı RMSE `6.7×10⁻⁵`
ve **kapsama yalnız r = 0.581**, yani köşe yarıçapının (0.721) %80'i.
Makale ayrıca §IX.C ve §X.B'de kapsamanın abartılmaması gerektiğini
özellikle vurguluyor. İlk bakışta site, makalenin desteklemediği daha
güçlü bir iddiada bulunuyor gibi göründü.

**Kontrol edildi ve şüphe ÇÜRÜDÜ.** Sitenin görselleri ayrı bir
yapılandırmadan üretiliyor: `python/sandbox/make_site_assets.py`, satır 140
`deg_est = [2., 3., 4., 5.]` ve satır 71'in yorumu *"full-field coverage,
so the estimate is constrained everywhere"*. Yani site, boardları
**bilerek tüm alana yayan** bir koşuyu anlatıyor; makale §IX.B ise kısmi
kapsamalı bir koşuyu. İkisi farklı deneyler, ikisi de kendi içinde doğru.

Betik bu oturumda koşuldu:

```
est_c=[0.0088, -0.8427, 0.2934, 0.2032]   r_cov=0.721   RMSE=3.97e-05
```

* `RMSE = 3.97×10⁻⁵` → sitenin "4.0×10⁻⁵"i **doğru** (yuvarlanmış).
* `r_cov = 0.721` → bu **tam olarak görüntü köşesi yarıçapı**, yani
  "out to the image corner" ifadesi de **doğru**.
* Dereceler `[2, 3, 4, 5]` → siteyle **birebir**.

**Sonuç: sitede abartılı iddia yok.** Bu not, aynı şüphenin bir daha
zaman kaybettirmemesi için yazıldı.

## DOĞRULANAN — varlıklar tam

`index.html` ve `distortion-explorer.html`in başvurduğu **on üç yerel
dosyanın hepsi** depoda mevcut (on görsel, `paper.pdf`, iki sayfa).
Eksik varlık yok.

---

## Ne denetlenmedi

Site tarayıcıda açılıp **görsel olarak** incelenmedi; denetim bağlantı,
varlık ve iddia-kaynak eşlemesiyle sınırlı kaldı. Dış bağlantılar
(`eigenvision.ai`, `github.com/HeliumNitrate`, `opticaldistortionlab.com`)
ağ üzerinden sınanmadı.

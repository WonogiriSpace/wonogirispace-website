---
title: "Berkenalan Dengan Constraint Layout di Android"
description: "Berkenalan Dengan Constraint Layout di Android"
date: 2024-05-10
image: "/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-1.png"
categories: ["Android", "Application Development"]
authors: ["Ageng"]
tags: ["android", "mobile", "development"]
draft: false
---

Layout yang didalamnya ada layout, didalamnya ada layout lagi, yang didalamnya ada layout juga. Hmm…

Saya sering sekali membuat layout semacam itu ketika develop aplikasi android. Terutama menggunakan LinearLayout dengan  _layout_weight_nya, Karena cukup praktis dan mudah dipahami oleh saya yang masih pemula. Sampai akhirnya  saya  menyadari ada Warning yang selalu keluar setiap saya membuat layout semacam itu, kalau tidak salah bunyinya :

_“Nested Weight are bad for performance”_

Well, biasanya saya tidak menghiraukan warning, yang saya pedulikan cuma Error, hehe. Tapi karena sering sekali muncul, akhirnya saya terpancing untuk googling tentang hal tersebut. Saat itulah saya bertemu dengan ConstraintLayout.

Eh, e_nggak ding._ Sebenarnya ketika kita membuat Activity baru di  **Android Studio**, Layout yang digenerate akan secara otomatis menggunakan ConstraintLayout. Tapi saya  _auto-ganti_  jadi LinearLayout atau RelativeLayout sesuai kebutuhan, hehe.

# Memahami ConstraintLayout

Sebenarnya ConstraintLayout mirip dengan RelativeLayout, karena letak View bergantung pada View lain dalam satu Layout ataupun dengan Parent Layoutnya. Contohnya di RelativeLayout kita bisa meletakkan sebuah View di atas, bawah, atau samping View lain. Kita juga dapat mengatur posisinya berdasarkan Parent Layout menggunakan tag seperti centerVertical, alignParentBottom, dll. tapi ConstraintLayout jauh lebih Fleksibel dan lebih mudah digunakan pada  **Layout Editor**.

Bayangkan seperti ini, pada ConstraintLayout, setiap View memiliki tali (Constraint) yang menarik tiap sisinya, yang mana tali tersebut bisa kita atur Elastisitas, Margin, dsb. Tali tersebut wajib kita “ikatkan” kepada anchor point atau suatu titik yang dapat berupa sisi dari Parent Layout, View lain, ataupun titik bantu (helper) yang bisa kita buat sendiri.

Tanpa constraint tersebut, sebuah Layout secara default akan terletak di posisi [0,0] (sebelah kiri-atas), sehingga sebuah View paling tidak membutuhkan 2 Constraint untuk sisi X dan sisi Y.

![\[Constraint Layout\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-2.png)

Pada gambar diatas, di **Layout editor**, Layout terlihat normal. Namun jika diperhatikan, View C tidak memiliki Vertical Constraint. Jika di render, View C akan sesuai Horizontal Constraintnya (sisi kiri dan kanan View A), tapi terletak di bagian atas Parent Layout (titik 0).

![\[Constraint Layout\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-3.png)

Untuk yang satu ini, View C sudah diberi Vertical Constraint, sehingga ketika di render, Posisinya akan sesuai seperti pada **Layout Editor**.

![\[Constraint Layout\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-1.png)

Untuk membuat constraint, setelah menambahkan View kedalam ConstraintLayout, akan muncul 4 titik constraint yang bisa dikaitkan pada Anchor Point, baik Vertical maupun Horizontal. Gambar diatas adalah contoh mengaitkan horizontal constraint bagian kiri kepada Parent Layout.

Menggunakan constraint tersebut, kita bisa membuat berbagai macam “Teknik Pengaitan” (_halah oposih_) sesuai kebutuhan, antara lain :

# **Parent**

![\[Parent\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-4.png)

Kita bisa mengaitkan constraint pada Parent Layout, kemudian mengatur jaraknya menggunakan Margin. Pada gambar di samping, Bagian kiri View A dikaitkan pada sisi kiri Parent Layout.

# **Posisi View**

![\[Posisi View\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-5.png)

Kita bisa mengatur urutan posisi dari View yang dibuat. Contoh pada gambar disamping, posisi View B akan selalu berada di sebelah kanan A, demikian pula View C, akan selalu berada di bawah View A. Namun karena tidak terdapat Alignment (atau constraint lawannya), View B masih bisa berpindah ke atas dan ke bawah, dan View C juga masih bisa berpindah ke Samping kiri dan kanan.

# **Alignment**

![\[Alignment\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-6.png)

Kita bisa membuat semacam Alignment pada View. Contohnya pada gambar disamping, sisi kiri View B segaris dengan View A. Untuk membuat Align Center, cukup buat dua buah Constraint (kiri dan kanan) kemudian kaitkan dengan masing-masing sisinya. Sebenarnya kita bisa membuat ini secara otomatis dengan cara memilih semua View yang ingin diatur Alignmentnya, kemudian klik menu  **Align**  pada  **Toolbar**, lalu pilih Alignment yang diinginkan.

# **Baseline Alignment**

![\[Baseline Alignment\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-7.png)

Misal kita ingin mengatur agar Sebuah TextView segaris dengan TextView lain di Layout yang berbeda, kita bisa menggunakan Baseline Alignment. Untuk membuatnya, pilih TextView yang ingin diatur baselinenya, kemudian klik tombol  **Edit Baseline**  yang muncul dibawahnya. Setelah itu tinggal tarik saja Baseline nya ke tujuan. Pada gambar di samping, TextView B dibuat segaris dengan TextView A menggunakan Baseline Alignment.

# **Guideline**

![\[Guideline\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-8.png)

Guideline adalam semacam Garis bayang yang tidak terlihat oleh User. Untuk membuatnya, klik tombol  **Guidelines**  pada  **Toolbar**, kemudian pilih  **Add Vertical Guideline**  atau  **Add Horizontal Guideline**  sesuai Kebutuhan. Kita bisa mengatur posisinya berdasarkan Dimension (dp) ataupun dengan Persentase (berdasarkan sisi layout). Kemudian kita bisa mengaitkan Constraint View kepada Guideline tersebut.

# **Barrier**

![\[Barrier\]](/images/posts/berkenalan-dengan-constraint-layout/constraintlayout-9.png)

Barrier hampir mirip dengan Guideline, bedanya Barrier tidak berdiri sendiri. Posisi barrier bergantung pada View didalamnya. Contoh kasusnya adalah apabila kita ingin membuat posisi View relatif terhadap beberapa (lebih dari satu) View lain.

Untuk membuat Barrier, klik tombol  **Guidelines**  pada  **Toolbar**, kemudian pilih  **Add Vertical Barrier**  atau  **Add Horizontal Barrier**  sesuai Kebutuhan. Pada  **Component Tree**, pilih View yang ingin dimasukkan kedalam Barrier tersebut. Kita bisa mengatur opsi dari Barrier seperti  **barrierDirection**  pada  **Window Attribute**. Pada gambar di samping, barrier di atur posisinya menjadi “end” atau “right”, sehingga menyesuaikan sisi paling kanan dari View yang ada di dalamnya.

Hmm, sebenarnya masih banyak sekali variasi yang bisa kita buat menggunakan ConstraintLayout, seperti mengatur Size, Ratio, Bias, dsb. tapi mungkin akan saya bahas di Artikel lain.
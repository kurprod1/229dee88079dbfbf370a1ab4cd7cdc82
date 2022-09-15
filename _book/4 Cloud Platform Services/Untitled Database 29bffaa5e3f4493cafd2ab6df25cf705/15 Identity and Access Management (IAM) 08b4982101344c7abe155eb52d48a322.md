# 15. Identity and Access Management (IAM)

Created: July 19, 2022 10:20 AM

# **Apa itu IAM ?**

**AWS Identity and Access Management (IAM)** merupakan sebuh layanan yang memungkinkan kita untuk mengelola akses layanan AWS dan sumber daya secara aman. Dengan menggunakan IAM, kita dapat membuat dan mengelola user dan group AWS, serta mengelola izin untuk memperbolehkan atau menolak akses mereka ke sumber daya AWS.

# **Fungsi dan Kegunaan IAM**

**AWS IAM** memiliki banyak sekali kegunaan, salah satunya adalah pengelolaan akses. Kita dapat menetapkan ***security credentials*** (kunci akses dan perangkat multi-factor authentication) untuk memberikan akses sumber daya AWS kepada user. Kita juga dapat mengatur layanan mana yang bisa diakases oleh user tersebut.

[*Ilustrasi Penggunaan IAM*](https://lh4.googleusercontent.com/Oa2om739xFR-lG46OoGj5Lrkc1IABopbd1tgVuUcz1I4gYlB9bxsiFARsV5H3ulO2s1XQ4K3c81_1-V7z8-ZBcUgk-Ys8iMRqkdq7kaNkPINVaZyA-XvHhoRDNqnjWMlvXdnVWIzGUKEz7BG2yKIbQ)

*Ilustrasi Penggunaan IAM*

Seperti salah satu contoh gambar diatas, dimana kita memiliki 3 user yaitu programmer, data engineer, dan DevOps. Mereka diatur oleh IAM agar dapat memanage layanan mereka sesuai kebutuhan, sehingga Programmer hanya bisa mengakses Elastic BeanStalk dan tidak bisa mengakses Amazon RDS dan Amazon VPC. Begitupun dengan data Engineer.

Selain itu kita juga dapat mengaktifkan access key ID untuk mendapatkan izin akses ke layanan AWS Management Console, AWS API dan sumber daya melalui AWS CLI. Sehingga nantinya setiap aktifitas kita bisa lakukan dari user yang kita gunakan.

# **Fitur IAM**

IAM sendiri memiliki beberapa fitur didalamnya yang dapat kita temui sebagai berikut.

## **Akses Kontrol Ketat pada AWS**

IAM memungkinkan pengguna mengontrol akses Layanan API AWS dan sumber daya khusus. IAM juga memungkinkan kita untuk menambahkan kondisi khusus semacam jam untuk mengontrol bagaimana pengguna dapat menggunakan AWS, alamat IP asal mereka, apakah mereka menggunakan SSL, atau telah mengautentikasi menggunakan perangkat dengan multi-factor authentication.

## **Multi-Factor Authentication**

Kita dapat melindungi AWS dengan menggunakan MFA (Multi-Factor Authentication). Dengan menggunakan MFA pengguna harus membuktikan kepemilikan fisik berupa token MFA atau perangkat ponsel yang didukung-MFA dengan memberikan kode MFA yang valid ketika ingin melakukan login pada AWS.

## **Mengelola Akses Kontrol Aplikasi**

Kita dapat mengaktifkan aplikasi ponsel berbasis browser untuk mengakses secara aman sumber daya AWS, dengan meminta kredensial keamanan sementara yang memberikan akses hanya pada sumber daya AWS khusus untuk periode waktu yang dapat dikonfigurasi.

## **Integrasi dengan Directori Perusahaan**

IAM dapat digunakan untuk memberikan karyawan dan aplikasi kita akses gabungan pada AWS Management Console dan layanan AWS API.

# **Setup IAM**

Pada bagian ini kita akan melakukan setting konfigurasi pada layanan IAM. Kita akan coba membuat beberapa user dan juga group, memisahkan antar user sesuai group dan kebutuhan yang akan mereka dapatkan.

## **Membuat IAM Group**

Pada pembahasan awal kita akan membuat sebuah **Group IAM** baru, fungsinya supaya kita bisa mengklasifikasikan sebuah user baru agar mendapatkan layanan yang sesuai dengan kebutuhan/perkerjaan yang mereka tekuni. Seperti contoh sorang programmer yang mungkin akan diberikan sebuah group IAM yang dapat mengakses beanstalk, S3, RDS, dll.

Hal pertama yang harus kita lakukan adalah masuk ke **IAM dashboard console** dengan memilih menu **service** lalu cari **IAM**.

[https://lh4.googleusercontent.com/ZYAD6g8UnI1j3i2RTUAgACOmaU1osJ9bS71kmBWUb4mwa4oSYWBQBHyvClxJyhXWRmFWfsZTB-pgFm1nlZkM0MLIqrkUFdweor9zuOB7FI2g6OgoFzHiLVuQUnJR12J8U20YmvnpOdPAQuhTGUan8A](https://lh4.googleusercontent.com/ZYAD6g8UnI1j3i2RTUAgACOmaU1osJ9bS71kmBWUb4mwa4oSYWBQBHyvClxJyhXWRmFWfsZTB-pgFm1nlZkM0MLIqrkUFdweor9zuOB7FI2g6OgoFzHiLVuQUnJR12J8U20YmvnpOdPAQuhTGUan8A)

Setelah kita masuk kedalam menu **dashboard IAM**, sekarang kita pilih menu **Groups** yang ada di samping kiri **dashboard IAM**.

[https://lh3.googleusercontent.com/ojdQJY2_cRR1esRRby7b6KzkwWL4Jlafh2B9_nU2w9AaHrysNMs0EipiN_9GUawAdXHDt2POOnv_b2WahVJ0-y7ye4q4kZcKsu66SodMS9Xf0msB6m2RhS9LaLC6tkCe364yQ9eKUFb_K9fEnYJ5kw](https://lh3.googleusercontent.com/ojdQJY2_cRR1esRRby7b6KzkwWL4Jlafh2B9_nU2w9AaHrysNMs0EipiN_9GUawAdXHDt2POOnv_b2WahVJ0-y7ye4q4kZcKsu66SodMS9Xf0msB6m2RhS9LaLC6tkCe364yQ9eKUFb_K9fEnYJ5kw)

Setelah itu bisa kita lihat groups menu yang kosong yang sudah ada groupnya. Untuk mulai mebuat Group pilih tombol **Create New Groups** yang ada diatas menu.

[https://lh3.googleusercontent.com/5pCuX3q6VKTD3H8beBYDhZb4lZ1g__AvceG-y7i4EVgQXMtBcfj4Z9dAMvnXR7NV5kh23u3flIDJwd4uwR_pMWT4wcf-ncT9wh99z5IqSep1J8H6Q5sFZ_41ie1iS9pPlKUwJgEqF0U0zex3_e6l_w](https://lh3.googleusercontent.com/5pCuX3q6VKTD3H8beBYDhZb4lZ1g__AvceG-y7i4EVgQXMtBcfj4Z9dAMvnXR7NV5kh23u3flIDJwd4uwR_pMWT4wcf-ncT9wh99z5IqSep1J8H6Q5sFZ_41ie1iS9pPlKUwJgEqF0U0zex3_e6l_w)

Setelah itu masukan nama Groups yang akan kita buat, disini saya membuat group baru dengan nama **DevOps** lalu klik **Next Step**.

[https://lh3.googleusercontent.com/cP7hU1WWJWMFucra8OJ1YSULh__4Dm9flp8qi5AN4T5ZQouG0xiO_mTY-900EgsipLyJCqIXMu7M3OumYT90RUF-cDwSq5JAo91Q6ZPRLSZwbfG7N6negyAx3Q3fLhl6yvn2tS3d1t3K1wew5VTCww](https://lh3.googleusercontent.com/cP7hU1WWJWMFucra8OJ1YSULh__4Dm9flp8qi5AN4T5ZQouG0xiO_mTY-900EgsipLyJCqIXMu7M3OumYT90RUF-cDwSq5JAo91Q6ZPRLSZwbfG7N6negyAx3Q3fLhl6yvn2tS3d1t3K1wew5VTCww)

Masuk kedalam menu Attach Policy, disini kita masukan policy mana yang akan kita berikan kepada group tersebut. Policy ini semacam hak akses layanan pada IAM, disini kita akan berikan **AdministrasionAccess**. Setelah itu klik **Next Step**.

[https://lh4.googleusercontent.com/smyAOFC798cVYwXr4hKODXaJ8JBaYAHsokknb3tYjzjDUS8w-R6KckJQqiJhIXj8f7VGQdYR8vV7bpgBRFO-cTRfeqhvEnFVlYMWZCoHxY3l7Wik1w-CE_I0DpT_G-2iaMNxwz-9R0_E9pJDmgiyAQ](https://lh4.googleusercontent.com/smyAOFC798cVYwXr4hKODXaJ8JBaYAHsokknb3tYjzjDUS8w-R6KckJQqiJhIXj8f7VGQdYR8vV7bpgBRFO-cTRfeqhvEnFVlYMWZCoHxY3l7Wik1w-CE_I0DpT_G-2iaMNxwz-9R0_E9pJDmgiyAQ)

Selanjutnya kita akan diberikan review dari hasil konfigurasi yang sudah kita lakukan, untuk melanjutkan untuk menyimpan Group kita klik **Create Group**.

[https://lh5.googleusercontent.com/IscXxe2-HePja1xTGD_iMLX1xjvASCQXegB8c_l5-ohS8XISZG0OyOAkwW-pgQJjjZWmt8OhB_ZExC1xqQkYANNyli43Yejty9PfHVW99W7-Ikkg363L3Qy7cy6j93PKzKGDn0iRUKSRxevvLDTucA](https://lh5.googleusercontent.com/IscXxe2-HePja1xTGD_iMLX1xjvASCQXegB8c_l5-ohS8XISZG0OyOAkwW-pgQJjjZWmt8OhB_ZExC1xqQkYANNyli43Yejty9PfHVW99W7-Ikkg363L3Qy7cy6j93PKzKGDn0iRUKSRxevvLDTucA)

Setelah berhasil, kita bisa lihat hasilnya seperti dibawah ini.

[https://lh4.googleusercontent.com/JnNZnoSmgXOHWrm97bwEKEmvKp0HTCNTMgE2-u4uSF4ZXd86UcqwGfR_OCZQAybiJA_Znxelo4wAXbrjWa1bH1EfKNo3O_w8j431s3zl-TEY4woxkKxRILoOucxDT5JWyHzSViRpkVUFLUl2FxvszA](https://lh4.googleusercontent.com/JnNZnoSmgXOHWrm97bwEKEmvKp0HTCNTMgE2-u4uSF4ZXd86UcqwGfR_OCZQAybiJA_Znxelo4wAXbrjWa1bH1EfKNo3O_w8j431s3zl-TEY4woxkKxRILoOucxDT5JWyHzSViRpkVUFLUl2FxvszA)

Dengan ini kita sudah membuat sebuah group untuk Administrasion Access, group ini nantinya akan kita masukan user yang akan memiliki hak akses sesuai dengan Group DevOps tersebut.

## **Membuat IAM User**

Setelah membuat Groups baru pada IAM, sekarang kita akan coba untuk membuat user baru. Cara membuatnya cukup mudah sekali, kita hanya perlu memilihi menu **Users** yang ada disamping dan kita akan diarahkan kedalam tampilan user.

[https://lh4.googleusercontent.com/gxVN68hV1O0xUTR-dPT8UveJlBEgBccnGqgoTWuY5RGILrTdEdpTu8eNWXxiXYLZ5gao3fWF8j3cxvazsxq9kN_Xht4HkASZgQmTbNsftCKpmcvlyoPVR-34-9QUnY6JAWceGIxMtal3dhA9pZv0IA](https://lh4.googleusercontent.com/gxVN68hV1O0xUTR-dPT8UveJlBEgBccnGqgoTWuY5RGILrTdEdpTu8eNWXxiXYLZ5gao3fWF8j3cxvazsxq9kN_Xht4HkASZgQmTbNsftCKpmcvlyoPVR-34-9QUnY6JAWceGIxMtal3dhA9pZv0IA)

Setelah itu klik **Add User** untuk membuat user baru, dan kita akan diarahkan ke menu setup.

Isikan Username, kemudian centang Programatic Access dan AWS Management Console access. Kemudian kita masukkan password atau bisa juga di generate password, kemudian centang require password reset lalu klik **Next Permission** seperti gambar berikut.

[https://lh5.googleusercontent.com/WCC7Xr2vXRetWQvG6GpQgKt9_Dzx2Kl5m2x3AJeW5pxc9Q8803C4stiVYxhXfLmDudQCStkLGzYjMN-tjWHSCmOS4gLmy8iBTsdoRUyrvUV75sDbYqpkvTBQCHtvaaWHr1meFji_Y6IxzaO9USfcKw](https://lh5.googleusercontent.com/WCC7Xr2vXRetWQvG6GpQgKt9_Dzx2Kl5m2x3AJeW5pxc9Q8803C4stiVYxhXfLmDudQCStkLGzYjMN-tjWHSCmOS4gLmy8iBTsdoRUyrvUV75sDbYqpkvTBQCHtvaaWHr1meFji_Y6IxzaO9USfcKw)

Selanjutnya kita masuk kedalam menu permission, disini kita pilih **Groups** yang sudah kita buat sebelumnya yaitu **DevOps** seperti dibawah ini.

[https://lh3.googleusercontent.com/yyURECYUyyma-vJo5PeagE1fIxMy6dcoQqgb8WHWVL0Iboiek6HkYzQqtPk1GMaPDDNmY1DdxfLoUeWJPWU__QEyXSGzwffR9xTGsq31iJ73Z58uX2AqJWjGPCkjTMRuUplG8aaqTUHJ6dtxL38i6A](https://lh3.googleusercontent.com/yyURECYUyyma-vJo5PeagE1fIxMy6dcoQqgb8WHWVL0Iboiek6HkYzQqtPk1GMaPDDNmY1DdxfLoUeWJPWU__QEyXSGzwffR9xTGsq31iJ73Z58uX2AqJWjGPCkjTMRuUplG8aaqTUHJ6dtxL38i6A)

Selanjutnya masuk kedalam menu review, disini kita akan diberikan review dari hasil yang sudah kita konfigurasi sebelumnya. Untuk melanjutkan pilih **Create User**.

[https://lh3.googleusercontent.com/_6DUtRzmbdVSACgmqh1VMdEpyMRI50-npls4wHewoUW4bjnyixGquy6rm_FqiWExNwJ8tawgcatXPLSSOZd-WkFDN87OSAS8dxZdu-RlAxRXaYB_eayTCmIvZlajRCtQwTOpJi0ilfKxJi_7-bIAxA](https://lh3.googleusercontent.com/_6DUtRzmbdVSACgmqh1VMdEpyMRI50-npls4wHewoUW4bjnyixGquy6rm_FqiWExNwJ8tawgcatXPLSSOZd-WkFDN87OSAS8dxZdu-RlAxRXaYB_eayTCmIvZlajRCtQwTOpJi0ilfKxJi_7-bIAxA)

Setelah berhasil maka akan muncul seperti gambar seperti dibawah ini. Untuk melakukan akses melalui AWS-CLI maka kita perlu mencatat access key ID dan juga secret access key, atau bisa juga di download sebagai CSV.

[https://lh6.googleusercontent.com/No84YrD-B6bQBo2a_eMywG385n-PsRYHXGYJTA416PWnl5u6mGxl5QJTtkAv1ol5oFEzzdiX__3_b906OZM73tWiMiNgIcdnCH17_Of9iWD5gi4L4URIZGOseHvCLoDxZRK1_we6uMDnnZ2LEyVKGQ](https://lh6.googleusercontent.com/No84YrD-B6bQBo2a_eMywG385n-PsRYHXGYJTA416PWnl5u6mGxl5QJTtkAv1ol5oFEzzdiX__3_b906OZM73tWiMiNgIcdnCH17_Of9iWD5gi4L4URIZGOseHvCLoDxZRK1_we6uMDnnZ2LEyVKGQ)

Access key ID dan Secret Access key ini merupakan key yang bisanya kita gunakan untuk melakukan akses AWS Config melalui CLI. Kita bisa membuat maksimal 2 Access Key setiap user IAM nya.

## **Testing Login Menggunakan IAM credentials**

Setelah kita membuat konfigurasi Groups dan User baru, sekarang saatnya kita mencoba kedua komponen yang sudah kita setting tersebut. Kita hanya perlu mengakses alamat IAM users sign-in link yang ada di **Dashboard IAM**.

[https://lh3.googleusercontent.com/5DKwvJdJia7msB4PQJYD-QCwDI-2OkZKIhf3ro5AgYB_9pO6CIwuKkkkopnNxLATbhBbNkhHgSrO2ko7B6tvvV5T9lc_I4G52-Px7j2hQk_sTk5ahVbEMyPwzElUrjpahqAb79uqqYt7Huoi0BzBEQ](https://lh3.googleusercontent.com/5DKwvJdJia7msB4PQJYD-QCwDI-2OkZKIhf3ro5AgYB_9pO6CIwuKkkkopnNxLATbhBbNkhHgSrO2ko7B6tvvV5T9lc_I4G52-Px7j2hQk_sTk5ahVbEMyPwzElUrjpahqAb79uqqYt7Huoi0BzBEQ)

Setelah kita akses maka akan muncul form login kepada **AWS Management Console** seperti berikut ini. Masukan user dan password yang sudah kita buat sebelumnya lalu klik **Sign in.**

[https://lh5.googleusercontent.com/E9ogSoNwD0ZWZG6GyMjiuTQJVuj940u8-UMffD5yalv1QFYW7Pd7BLBKUe9Ztz2oo22YT7IYMK_PnR8zB5YXL6VE9mSRMVWlaAN6DgybOO9jNGgPZ3Joz-jQKArFApZxuwkVbmza7G6DkJI_E02mpQ](https://lh5.googleusercontent.com/E9ogSoNwD0ZWZG6GyMjiuTQJVuj940u8-UMffD5yalv1QFYW7Pd7BLBKUe9Ztz2oo22YT7IYMK_PnR8zB5YXL6VE9mSRMVWlaAN6DgybOO9jNGgPZ3Joz-jQKArFApZxuwkVbmza7G6DkJI_E02mpQ)

Karena kita tadi menceklik permintaan untuk mereset password, maka akan muncul form untuk mengubah password dari akun user kita. Ubah password sesuai kita inginkan.

[https://lh6.googleusercontent.com/Szk7R5bTVtzEQ056M2H5cBcLIoEAO-8FrIhpHBHFj3mf6zcY4TsWh9l1zcG2yyh9KyNJ9ZpeRLlnWqcaF9xY_-o5Ter0a1PUExsLUIkvBOKfZdpjcoQ08A-m04_nmkuYCCpnt9trccI3WJjHZbS_uQ](https://lh6.googleusercontent.com/Szk7R5bTVtzEQ056M2H5cBcLIoEAO-8FrIhpHBHFj3mf6zcY4TsWh9l1zcG2yyh9KyNJ9ZpeRLlnWqcaF9xY_-o5Ter0a1PUExsLUIkvBOKfZdpjcoQ08A-m04_nmkuYCCpnt9trccI3WJjHZbS_uQ)

Setelah berhasil login, kita akan diarahkan langsung kedalam dashboard AWS Management Console seperti biasanya.

[https://lh3.googleusercontent.com/Hf5oU7TEeU3xsmXuNW6VSt-reAnP_wVL8HSsV7sBFHemUbuAngmN4dk9i8JqLbGpgOzBDBd3cMpIKYAOeOYPASAXXmuab97b5oNWizkkv5CCX3wY3n-hn1fZV1iNzDqLilr8TCvT-FU-ug2t9tyFtg](https://lh3.googleusercontent.com/Hf5oU7TEeU3xsmXuNW6VSt-reAnP_wVL8HSsV7sBFHemUbuAngmN4dk9i8JqLbGpgOzBDBd3cMpIKYAOeOYPASAXXmuab97b5oNWizkkv5CCX3wY3n-hn1fZV1iNzDqLilr8TCvT-FU-ug2t9tyFtg)

Dengan begini kita sudah mendapatkan sebuah user baru yang bisa kita gunakan, kita bisa buat beberapa user lain untuk keperluan service yang lain juga seperti untuk management ECS, VPC, maupun Storage S3 saja.

## **Mengubah Alamat Login IAM**

Sebelumnya kita sudah membuat Group, user dan mencobanya sendiri dengan melakukan login pada Management Console AWS. Akan tetapi alamatnya yang panjang dan berupa angka akan membingungkan kita pada saat ingin melakukan akses ke AWS tersebut.

Maka kita perlu mengubah alamat tersebut agar mudah untuk diakses. Caranya cukup mudah, kita hanya perlu masuk ke IAM Dashboard lalu klik **Edit.**

[https://lh3.googleusercontent.com/OhZslLsgiw9Pa0XwRWuCh47YMST5iQ5xfLnu75Kdd_45OcRXaIT05s5_RcDTsyHvYPkGtiSPzf4LBlU_I7ch2JkuYtAVuTGfmiegWDl38K4Fg-BODyZ2lmPD1Y_0Q193rG-54Fi8ZmrFF6nhV1boDg](https://lh3.googleusercontent.com/OhZslLsgiw9Pa0XwRWuCh47YMST5iQ5xfLnu75Kdd_45OcRXaIT05s5_RcDTsyHvYPkGtiSPzf4LBlU_I7ch2JkuYtAVuTGfmiegWDl38K4Fg-BODyZ2lmPD1Y_0Q193rG-54Fi8ZmrFF6nhV1boDg)

Setelah itu akan muncul pop out untuk kita mengisikan name alias dari DNS IAM user yang akan kita gunakan seperti berikut. Klik **Save** untuk menyimpan.

[https://lh6.googleusercontent.com/PdQPrueMe9WjRyblj_jIS_yvcgHybamjqh0iyqGyKyFQOD5NFm9xLU0jnr45VRTpHOvliRV_e92jYpeAD1b6QnGEgJr3omWyiw4iwYeiuy90sMY8dcATo7ko96tjI1OZLMvtevB-8foXk_r74Zp_IA](https://lh6.googleusercontent.com/PdQPrueMe9WjRyblj_jIS_yvcgHybamjqh0iyqGyKyFQOD5NFm9xLU0jnr45VRTpHOvliRV_e92jYpeAD1b6QnGEgJr3omWyiw4iwYeiuy90sMY8dcATo7ko96tjI1OZLMvtevB-8foXk_r74Zp_IA)

Maka alamat DNS IAM pun akan berubah sesuai dengan yang sudah kita buat seperti ini.

[https://lh5.googleusercontent.com/aD8-il41mC_c8mVb_sXKCFKXySFLJ5olAj-eTLefwj7mLPOsWxVR9z4PpnPcmHA-_3yGMAPpqMJeEEbyIJV3LjIqgWWBpCsnfJKIW-udyZvNhrS_qdW0jiAH7XseERdkn-KJwba1x-JCsaHfo-pMUA](https://lh5.googleusercontent.com/aD8-il41mC_c8mVb_sXKCFKXySFLJ5olAj-eTLefwj7mLPOsWxVR9z4PpnPcmHA-_3yGMAPpqMJeEEbyIJV3LjIqgWWBpCsnfJKIW-udyZvNhrS_qdW0jiAH7XseERdkn-KJwba1x-JCsaHfo-pMUA)

Setelah itu copy link tersebut lalu coba akses di browser, maka kita akan langsung diarahkan ke alamat login dengan ID yang sudah otomatis terisi dengan alamat Alias dari IAM user sign-in link.

![*Hasil perubahan alamat Login IAM*](15%20Identity%20and%20Access%20Management%20(IAM)%2008b4982101344c7abe155eb52d48a322/Untitled.png)

*Hasil perubahan alamat Login IAM*
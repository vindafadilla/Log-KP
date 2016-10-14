#Dokumentasi API QePon Square

##Anode API

###Add New API
#### Request
Requires token-based authentication.

	POST /api/v1/auth/api/add

#### Mandatory Parameters :

* `api_code` : api code name, Mandatory
* `api_uri` : api uri. example : /api/v1/auth/api/add . Please look at runner.go. This api_uri must be valid since rbac need this parameter to validate whether user can access defined api or not. Mandatory

#### Response

* `400` : invalid request parameter
* `409` : duplicate api, api must be unique
* `500` : internal server error 
* `201` : created

#### Proses
1.  Deklarasi variabel APIRequest yang merepresentasikan request untuk API baru.
	APICode string `json:"api_code" binding:"required"`
	URI     string `json:"api_uri" binding:"required"`
2. Pembuatan Info Log dan inisialisasi database
3. Data binding untuk APIReqisterRequest. Jika terdapat error akan terdapat pesan "Error when binding request, reason = " dengan penjelasan error yang di dapatkan melalui log
4. Memvalidasi API belum tidak terduplikasi dengan mengecek ke database. Jika API yang ingin dibuat telah ada sebelumnya, maka akan terdapat pesan Duplicate API yang ditampilkan melalui log juga terdapat pesan melalui json.
5. Jika API tervalidasi, maka API akan terregister dan dimasukkan kedalam database yang terdapat pada method NewAnodeAPI. 
6. Jika semua langkah berhasil akan terdapat pemberitahuan melalui log dan akan memberikan response data json.

###Get API
#### Request :
Requires token based authentication.
	
	GET /api/v1/auth/api/get

#### Optional Parameters :

* `code` : apicode to be shown. 
* `apiid` : apiid to be shown
* `page` : Determines which page to be shown. Default to `1`.

#### Proses:
1. Deklarasi variabel. Pembatasan page dengan maximal entry 50 per page.
2. Inisialisasi database. 
3. Merequest query untuk URL .
4. Mengambil API code dari database dan menampungnya ke dalam variabel.
5. Mengambil API id dari database dan menampungnya ke dalam variabel.
6. Mengambil page dari database yang sebelumnya diubah terlebih dahulu dari string menjadi integer dan menampungnya ke variabel.
7. Membuild query, jika API Id dan API code tidak kosong, maka nilai dari API Id dan API code akan ditampung ke dalam variabel map,
8. Lalu, akan memberikan response berupa data json yang berisi data-data salah satunya API code dan API Id.

### Update API

#### Request :

Requires token based authentication.
	
	PUT /api/v1/auth/api/update

#### Mandatory Parameters :

* `api_id` : api id. You can get from get api request
* `api_code` : api code
* `api_uri` : api uri 

#### Response

* `400` : invalid request parameter(bad request)
* `409` : duplicate api, api must be unique
* `500` : internal server error 
* `200` : updated

#### Proses
1.  Deklarasi variabel APIPutRequest yang merepresentasikan request untuk API yang ingin di update.
	APIID   string `json:"api_id" binding:"required"`
	APICode string `json:"api_code" binding:"required"`
	URI     string `json:"api_uri" binding:"required"`
2. Pembuatan Info Log dan inisialisasi database
3. Data binding untuk update API Request. Jika terdapat error akan terdapat pesan "Error when binding request, reason = " dengan penjelasan error yang di dapatkan melalui log.
4. Memvalidasi API agar tidak terduplikasi dengan mengecek ke database. Jika API yang ingin di update telah ada, maka akan terdapat pesan Duplicate API yang ditampilkan melalui log juga terdapat pesan melalui json.
5. Jika API tervalidasi, maka API akan terupdate dan diperbaharui pada database. 
6. Karena kita telah mengupdate API maka user dan group juga harus di update dengan method baru yaitu updateGroupAndUserByNewAPI.
7. Selain user dan group, kita juga harus mengisi kembali access control untuk mengakses API.
8. Jika semua langkah berhasil akan terdapat pemberitahuan melalui log dan akan memberikan response data json.

### Delete API

#### Request :
Requires token based authentication
	DELETE /api/v1/auth/api/delete

#### Mandatory Parameters :

* `api_id` : id of api

#### Respon

* `404` : not found
* `500` : internal server error
* `200` : deleted

#### Proses
1.   Pembuatan Info Log dan deklarasi variabel APIDeleteRequest yang merepresentasikan request untuk menghapus API.
2. Inisialisasi database
3. Data binding untuk APIDeleteRequest . Jika terdapat error akan terdapat pesan "Error when binding request, reason = " dengan penjelasan error yang di dapatkan melalui log. Ini untuk mendapatkan data API mana yang akan dihapus.
4. Menghapus API dari database. Jika API yang ingin dihapus tidak ada sebelumnya, maka akan terdapat pesan Not found.
5. Setelah API dihapus, maka group dan user yang berhubungan dari API itu juga dihapus.
6. Jika semua langkah berhasil akan terdapat pemberitahuan melalui log dan akan memberikan response data json.

## Organization API

### Add New Organization

#### Request

Requires token-based authentication.

	POST /api/v1/organizations/add

#### Parameters :

* `name` : name of organization, Mandatory.
* `description` : description of group. Optional.
* `organization_code` : code of organization, Mandatory.
* `first_address` : first address, Optional.
* `second_address` : second address, Optional.
* `city` : city, Optional.
* `state` : state, Optional.
* `zip` : zip, Optional.
* `phone` : phone, Optional.
* `fax` : fax, Optional.
* `latitude` : latitude, Optional.
* `longitude` : longitude, Optional.

#### Response

* `201` : Created
* `400` : Bad request
* `500` : Internal server error

#### Proses
1. Pembuatan Info Log dan inisialisasi database.
2. Data binding untuk merequest pembuatan organisasi. Jika terdapat error akan terdapat pesan "Invalid request, error = " dengan penjelasan error yang di dapatkan melalui log.
3. Validasi data, terutama pada organization code, karena oraganization code tidak diperbolehkan menggunakan spasi.
4. Menambahkan user yang merequest pembuatan organisasi pada bagian createdby.
5. Menginsert ke dalam database organisasi yang akan dibuat pada method NewOrganization. Pada method tersebut juga, dibuat token untuk organisasi.
6. Jika semua langkah berhasil akan terdapat pemberitahuan melalui log dan akan memberikan response data json.

### Update Organization

#### Request

Requires token-based authentication.

	PUT /api/v1/organizations/update

#### Parameters :

* `id` : organization ID you want to update. Mandatory.
* `name` : name of organization, Optional.
* `description` : description of group, Optional.
* `organization_code` : code of organization. Mandatory.
* `first_address` : first address, Optional.
* `second_address` : second address, Optional.
* `city` : city, Optional.
* `state` : state, Optional.
* `zip` : zip, Optional.
* `phone` : phone, Optional.
* `fax` : fax, Optional.
* `latitude` : latitude, Optional.
* `longitude` : longitude, Optional.

#### Response

* `200` : OK
* `400` : Bad request
* `404` : Not found
* `500` : Internal server error

#### Proses
1. Pembuatan Info Log dan inisialisasi database, juga deklarasi struct UpdateOrganizationRequest. 
2. Data binding untuk merequest update pada data organisasi. Jika terdapat error akan terdapat pesan "Invalid request, error = " dengan penjelasan error yang di dapatkan melalui log.
3. Validasi data, terutama pada organization code, karena organization code tidak diperbolehkan menggunakan spasi.
4. Membuild update dari organization.
5. Mengupdate data organisasi yang ada pada database.
6. Proses selanjutnya sedikit berbeda antara branch master dan dev. Pada dev, ketika data pada database telah di update, maka data akan langsung meresponse data json. Sedangkan, pada branch master, setelah data pada database di update, maka akan di lakukan update juga terhadap collection yang berhubungan dengan organisasi tersebut seperti pada data user di bagian user profile yang merupakan anggota organisasi tersebut. Lalu, setelahnya baru meresponse data json.

### Delete Organization

#### Request

Requires token based authentication

	DELETE /api/v1/organizations/delete

#### Parameters

* `id` : organizationID, Mandatory.

#### Response

* `500` : Internal Server Error
* `404` : Not found
* `200` : OK

#### Proses
1. Pembuatan Info Log dan inisialisasi database.
2. Data binding untuk merequest penghapusan organisasi. Jika terdapat error akan terdapat pesan "Invalid request, error = " dengan penjelasan error yang di dapatkan melalui log.
3. Menghapus organisasi sesuai id yang digunakan organisasi ke dalam database organisasi. 
4. Mengupdate fields yang berhubungan dengan organisasi yang dihapus yang terdapat pada method deleteOrganizationRelatedFields, sehingga fields yang terdapat organisasi tersebut akan kosong.
6. Jika semua langkah berhasil akan terdapat pemberitahuan melalui log dan akan memberikan response data json.

### Get Organization

#### Request

Requires token-based authentication.

	GET /api/v1/organizations/get

#### Optional Parameters :

* `name` : organization name.
* `id` : organization id.
* `code` : organization code.
* `page` : page you want to showed.

#### Response

* `400` : Bad request
* `500` : Internal Server Error
* `200` : OK

#### Proses
1. Pembuatan Info Log, deklarasi variabel dan inisialisasi database.
2. Merequest query untuk URL
3. Mengambil nama dari organisasi di database dan menampungnya ke dalam variabel.
4. Mengambil id dari organisasi di database dan menampungnya ke dalam variabel.
5. Mengambil code dari organisasi di database dan menampungnya ke dalam variabel.
6. Mengambil page dari database yang sebelumnya diubah terlebih dahulu dari string menjadi integer dan menampungnya ke variabel.
7. Membuild query, jika nama, Id dan code dari organisasi tidak kosong, maka nilai dari nama, Id dan code akan ditampung ke dalam variabel map.
8. Lalu, akan memberikan response berupa data json yang berisi data-data salah satunya nama, code dan Id dari perusahaan.

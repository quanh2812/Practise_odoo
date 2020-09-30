# CIC EKYC

In this document, we'll working on this URL: http://cicfinaltest.bmpdev.kiuglobal.com. However, In Kiu BMP system, each customer will have their own URL so please leave a place to config the URL.

## Authentication

For security, every outbound request need to be verified by access_token which should be put in headers of every request.

> [POST] http://localhost:8069/get_token

### Headers

| Key          | Value            |
| ------------ | ---------------- |
| Content-Type | application/json |

### Request Parameters

| Key      | Type   | Description |   Mandatory   |
| -------- | ------ | ----------- | :-----------: |
| login    | String | Username    | :exclamation: |
| password | String | Password    | :exclamation: |

> Sample request

```json
{
    "jsonrpc": "2.0",
    "method": "call",
    "params": {
        "login": "admin",
        "password": "Ktrtx>2m"
    }
}
```

> Sample response

```json
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "success": true,
        "data": {
            "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1aWQiOjJ9.51azwAnFB3NQ1g_DX3gLkrHK8KUguyw17Wi6oiPJ1ug",
            "db_name": "cictest",
            "uid": 2
        }
    }
}
```

## Create Application Form

> [POST] http://cicfinaltest.bmpdev.kiuglobal.com/cic_ekyc/application/create

### Headers

| Key           | Value                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------ |
| Content-Type  | application/json                                                                                       |
| Authorization | Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOjQyfQ.99p3tb3L-vsoXtDORuR3Ql0Pa4WLr-oHndNSNLq71iI |

### Request Parameters

| Field | Description | Data Type | Mandatory |
| ---------- | -------- | ------------ | :--------: |
| name | Ho va ten | String | :exclamation: |
| date_of_birth | Ngay sinh | Date | :exclamation: |
| phone | Dien thoai | String | :exclamation: |
| email | Email | String | :exclamation: |
| city | Tinh (Thanh pho) | String | :exclamation: |
| district | Quan (Huyen) | String | :exclamation: |
| commune | Xa (Phuong) | String | :exclamation: |
| address | Dia chi | String | :exclamation: |
| document_type | Loai ho so | Boolean | :exclamation: |
| cmnd_code | So CMND | String | :exclamation: |
| date_issued | Ngay cap | Date | :exclamation: |
| issued_by | Noi cap | String | :exclamation: |
| other_document_type | CMND/CCCD khac | String |  |
| anh_mat_truoc | Anh mat truoc | Binary | :exclamation: |
| anh_mat_sau | Anh mat truoc | Binary | :exclamation: |
| anh_chan_dung | Anh mat truoc | Binary | :exclamation: |

> Sample request if "document_type" == "cccd"

```json
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "model": "res.bank",
    "method": "create",
    "args": [
      {
        "name": "Tạ Quốc Anh",
		"date_of_birth": "1997-12-28",
		"phone" : "0912281297",
		"email" : "anh@gmail.com", 
		"address" : "303, C4B",
		"commune" : "Thanh Cong",
		"district" : "Ba Dinh",
		"city" : "Ha Noi",
		"document_type" : "cccd",
		"cccd_code" : "001097012559",
		"date_issued" : "2020-09-02",
		"issued_by" : "Ha Noi",
		"anh_mat_truoc" : "image_based64",
		"anh_mat_sau" : "image_based64",
		"anh_chan_dung" : "image_based64",
      }
    ]
  }
}
```

> Sample request if "document_type" == "cmnd"

```json
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "model": "res.bank",
    "method": "create",
    "args": [
      {
        "name": "Tạ Quốc Anh",
		"date_of_birth": "1997-12-28",
		"phone" : "0912281297",
		"email" : "anh@gmail.com", 
		"address" : "303, C4B",
		"commune" : "Thanh Cong",
		"district" : "Ba Dinh",
		"city" : "Ha Noi",
		"document_type" : "cmnd",
		"cmnd_code" : "001097012559",
		"date_issued" : "2020-09-02",
		"issued_by" : "Ha Noi",
		"anh_mat_truoc" : "image_based64",
		"anh_mat_sau" : "image_based64",
		"anh_chan_dung" : "image_based64",
      }
    ]
  }
}
```

> Sample response

```json
{
  "jsonrpc": "2.0",
  "id": null,
  "result": 4 // id of the created bank
}
```
## Get List of Application Form

> [GET] http://cicfinaltest.bmpdev.kiuglobal.com/cic_ekyc/application/read

### Headers

| Key           | Value                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------ |
| Content-Type  | application/json                                                                                       |
| Authorization | Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOjQyfQ.99p3tb3L-vsoXtDORuR3Ql0Pa4WLr-oHndNSNLq71iI |

> Sample request

```json
{
  "jsonrpc": "2.0",
  "method": "call",
  "params": {
    "model": "application.form",
    "method": "read",
    "args": [],
    "kwargs": {
      "fields": ["name"]
    }
  }
}
```

> Sample response

```json
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "1": {
            "name": "Tạ Quốc Anh",
            "application_code": "CIC00001",
            "phone": "0922255562",
            "date_of_submit": "09-29-2020",
            "document_type": "cmnd",
            "state": "cho_tham_dinh"
        },
        "2": {
            "name": "Hoa Nguyen",
            "application_code": "CIC00002",
            "phone": "0322265599",
            "date_of_submit": "09-29-2020",
            "document_type": "cmnd",
            "state": "cho_tham_dinh"
        }
    }
}
```

## Edit Application Form

> [GET] http://cicfinaltest.bmpdev.kiuglobal.com/cic_ekyc/application/edit

### Headers

| Key           | Value                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------ |
| Content-Type  | application/json                                                                                       |
| Authorization | Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1aWQiOjQyfQ.99p3tb3L-vsoXtDORuR3Ql0Pa4WLr-oHndNSNLq71iI |

> Sample request

```json
{
    "jsonrpc": "2.0",
    "method": "call",
    "params": {
        "form_application": {
            "anh_mat_truoc": "image_based64"
        },
        "id": 2
    }
}
```

> Sample response

```json
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "success": true
    }
}
```




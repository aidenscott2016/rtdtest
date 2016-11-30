# Introduction

Welcome to the Pay4Later API

# Create an application

> The POST request body

```json
{
  "installation_id": 172,
  "unique_reference": "123456789",
  "finance": {
    "product": {
      "product_code": "ONIB12-19.9"
    },
    "goods": [
      {
        "description": "One way flight to nowhere",
        "price": 89900,
        "quantity": 1
      }
    ],
    "deposit": 20000
  },
  "consumer": {
    "title": "Mr",
    "forename": "Peter",
    "surname": "Money",
    "date_of_birth": "1972-05-24",
    "phone_number": "02077777666",
    "mobile_number": "07783909666",
    "email": "juan.guardianelli@pay4later.com",
    "marital_status": "cohabiting",
    "addresses": [
      {
        "house_number": "113",
        "street": "Ebury St.",
        "town": "London",
        "county": "London",
        "postcode": "SW1W 9QU"
      }
    ],
    "residential_status": "owner",
    "employment": {
      "salary": 45000,
      "status": "SelfEmployed",
      "employer":"pay4later",
      "occupation":"xbox360",
      "years_with_employer": 10
    }
  }
}
```
> To start an app, use this curl command:

```shell
curl -vvv 'http://localhost:8080/api/applications' \
  --data-binary '[[json body]]' \
-H 'Authorization: Bearer [[your authourisation key]]' \
-H 'Content-Type: application/json; charset=UTF-8' \
-H 'Connection: keep-alive'
```
> This will return an empty array and a header like 

```
 HTTP/1.1 201 Created
 Date: Wed, 30 Nov 2016 09:47:03 GMT
 Server: Apache/2.4.7 (Ubuntu)
 Access-Control-Allow-Methods: GET, POST, PATCH, PUT, DELETE
 Location: /api/applications/114135
 Content-Length: 2
 Keep-Alive: timeout=5, max=100
 Connection: Keep-Alive
 Content-Type: application/json; charset=utf-8
```

### HTTP Request

`POST http://localhost:8080/applications`

### Header Params
`Authorization: Bearer [[your access_token]]`

<aside class="warning">
Your <code>access_token</code> can be obtained from the <code>/request_token</code> endpoint.
</aside>


### Body
The content of the request is json formatted, this primarily holds the consumer data. Some of the variables that aren’t intuitive to understand are explained below.

<table class="table table-bordered table-hover table-condensed">
<tbody><tr>
<td>Request</td>
<td>Description</td>
</tr>
<tr>
<td>Identification-&gt;InstallationId</td>
<td>This will be used to decide where credit status notifications go to in testing but there will only be 1 static installation id in live.</td>
</tr>
<tr>
<td>Identification-&gt;RetailerUniqueReference</td>
<td>The E Agents&#39;s unique reference to tie applications to their system</td>
</tr>
<tr>
<td>Identification-&gt;ApplicationType</td>
<td>The type of application submitted, in this case it will be static as BL</td>
</tr>
<tr>
<td>Identification-&gt;ReturnUrl</td>
<td>The url the customer will return to after finishing the application process</td>
</tr>
<tr>
<td>Finance-&gt;Code</td>
<td>The code identifies the finance product used.</td>
</tr>
<tr>
<td>Finance-&gt;Deposit</td>
<td>Leave static as 0</td>
</tr>
<tr>
<td>Consumer-&gt;ResidentialStatus</td>
<td>Residential status code, possible entries and their descriptions:<br/>H (Home Owner)<br/>T (Tenant)<br/>L (Living with parents)<br/>C (Council Renting)<br/>O (Other)</td>
</tr>
<tr>
<td>Consumer-&gt;MaritalStatus</td>
<td>Marital status code, possible entries and their descriptions:<br/>M (Married)<br/>S (Single)<br/>C (Cohabiting)<br/>D (Divorced)<br/>P (Seperated)<br/>W (Widowed)</td>
</tr>
<tr>
<td>Consumer-&gt;Employment-&gt;Status</td>
<td>Employment status code, possible entries and their descriptions:<br/>P (Full Time)<br/>PT (Part Time)<br/>S (Self Employed)<br/>M (Military)<br/>R (Retired)<br/>H (Houseperson)</td>
</tr>
<tr>
<td>Consumer-&gt;PhoneNumber</td>
<td>Not required, but if set, must match the following regex:<br/>/(^+[0-9]{2}|^+[0-9]{2}(0)|^(+[0-9]{2})(0)|^00[0-9]{2}|^0)([0-9]{9}$|[0-9-\s]{10}$)/<br/>It will match local and both international formats:<br/>07123456789<br/>00447123456789<br/>+447123456789</td>
</tr>
<tr>
<td>Consumer-&gt;MobileNumber</td>
<td>Not required, but if set, must match the following regex:<br/>/(^+[0-9]{2}|^+[0-9]{2}(0)|^(+[0-9]{2})(0)|^00[0-9]{2}|^0)([0-9]{9}$|[0-9-\s]{10}$)/<br/>It will match local and both international formats:<br/>07123456789<br/>00447123456789<br/>+447123456789</td>
</tr>
<tr>
<td>AdditonalData-&gt;CustomerType</td>
<td>The type of customer, possible entries:<br/>&#39;Landlord&#39;<br/>&#39;Owner Occupier&#39;</td>
</tr>
<tr>
<td>AdditionalData-&gt;CustomerSaleType</td>
<td>The customer sale type, possible entries:<br/>&#39;Sale Only&#39;<br/>&#39;Sale and Purchase&#39;</td>
</tr>
<tr>
<td>Marketing-&gt;Lender</td>
<td>Opt out the lender marketing</td>
</tr>
</tbody></table>
  


# Kittens

## Get All Kittens


```curl
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten


```curl
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```


> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve


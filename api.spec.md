## APi Specification

<details>
<summary>
<code>POST</code> <code><b>/</b></code> <code>{identity-server}/signin</code>
</summary>

#### Headers

> | client_id | X-Auth-Token                      |
> | --------- | --------------------------------- |
> | 18700     | local-shr-system-admin_auth_token |


#### Body

> | email                           | password    |
> | ------------------------------- | ----------- |
> | local-shr-system-admin@test.com | thoughtwork |


#### Response:

{
   "access_token": "bdf2e1f9-ef49-4733-89cb-7ab3340c155f"
}

</details>

#### Create a new patient
<details>
<summary>
<code>POST</code> <code><b>/</b></code> <code>{mci-server}/api/v1/patients<code>
</summary>
</details>

#### Get a Patient By Health ID

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients/{hid}<code>
</summary>
</details>

#### Update a Patient with Health ID

<details>
<summary>
<code>PUT</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients/{hid}<code>
</summary>
</details>

#### a. Search a Patient by primary identifiers - National ID, Birth Regd No
##### For nid

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients?nid={nid_number}<code>
</summary>
</details>

##### For BRN

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients?bin_brn={bin_brn_number}<code>
</summary>
</details>

##### For UID

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients?uid={uid}<code>
</summary>
</details>

#### b. Search Patient by secondary identifiers -  phone number, household code

##### For PhoneNo

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients?phone_no={phone_no}<code>
</summary>
</details>

##### For HouseHold code

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients?household_code={household_code}<code>
</summary>
</details>

#### c. Search Patient name or location within an area.

##### For Name within geo coded area

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients?given_name={given_name}&present_address={geolocation code}&sur_name={surname}<code>
</summary>
</details>

##### For  PhoneNo within geo coded area:

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients?phone_no={phone_no}&present_address={geolocation code}<code>
</summary>
</details>

##### For  HouseHold within area:

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/patients?household_code={household_code}&present_address={geolocation code}<code>
</summary>
</details>

#### Get All patient By Catchment 

<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{mci-server}/api/{version}/catchments/{geolocation code}/patients<code>
</summary>
</details>

#### Create an Encounter

<details>
<summary>
<code>POST</code> <code><b>/</b></code> <code>{shr-server}/patients/{health Id}/encounters<code>
</summary>


Headers :<br>

X-Auth-Token : {auth token returned from Identity Service Provider}<br>
client_id : {client id of requester in Identity Service Provider}<br>
From : {email_id of requester registered in Identity Service Provider}<br>
Content-Type: application/xml, application/json ;charset=utf-8

##### Sample Success Response

```
{
    "encounterId": "9f81a363-ede1-4bd0-8af2-eb73045c9ab1",
    "errors": [],
    "successful": true,
    "errorResult": null
}
```

##### Sample Failure Response

```

{
    "httpStatus": "422",
    "message": "Unprocessable entity : [{"field":"f:Encounter/f:patient","type":"invalid","reason":"http://mci-server/api/default/patients/9801098063:Patient Health Id does not match."}]",
    "errors": [
        {
            "field": "f:Encounter/f:patient",
            "type": "invalid",
            "reason": "http://mci-server/api/default/patients/9801098063:Patient's Health Id does not match."
        }
    ]
}
```

</details>

#### Update an Encounter

<details>
<summary>
<code>PUT</code> <code><b>/</b></code> <code>{shr-server}/patients/{health Id}/encounters/{encounter id}<code>
</summary>

Headers :<br>

X-Auth-Token : {auth token returned from Identity Service Provider}<br>
client_id : {client id of requester in Identity Service Provider}<br>
From : {email_id of requester registered in Identity Service Provider}<br>
Content-Type: application/xml, application/json ;charset=utf-8

##### Sample Success Response

```
{
    "encounterId": "9f81a363-ede1-4bd0-8af2-eb73045c9ab1",
    "errors": [],
    "successful": true,
    "errorResult": null
}
```
##### Sample Failure Response

```

{
    "httpStatus": "422",
    "message": "Unprocessable entity : [{"field":"f:Encounter/f:patient","type":"invalid","reason":"http://mci.twhosted.com/api/default/patients/9801098063:Patient Health Id does not match."}]",
    "errors": [
        {
            "field": "f:Encounter/f:patient",
            "type": "invalid",
            "reason": "http://mci.twhosted.com/api/default/patients/9801098063:Patient's Health Id does not match."
        }
    ]
}
```

</details>

#### Get all encounters for a patient.


<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{shr-server}/patients/{health Id}/encounters<code>
</summary>

##### Headers :

X-Auth-Token : {auth token returned from Identity Service Provider}<br>
client_id : {client id of requester in Identity Service Provider}<br>
From : {email_id of requester registered in Identity Service Provider}<br>
Accept: application/json(default) OR application/atom+xml

</details>

#### Get a specific encounter for a patient. 


<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{shr-server}/patients/{health Id}/encounters/{encounter id}<code>
</summary>

##### Headers :

X-Auth-Token : {auth token returned from Identity Service Provider}<br>
client_id : {client id of requester in Identity Service Provider}<br>
From : {email_id of requester registered in Identity Service Provider}<br>
Accept: application/json(default) OR application/atom+xml<br>

##### Sample Response

Response


> | http code | content-type | response            |
> |-----------|--------------|---------------------|
> | 412       |              |PRECONDITION_FAILED  |
> | 400       |              |BAD_REQUEST          |
> | 422       |              |UNPROCESSABLE_ENTITY |
> | 401       |              |UNAUTHORIZED         |
> | 403       |              |FORBIDDEN            |


</details>

#### Get all encounters for a catchment 


<details>
<summary>
<code>GET</code> <code><b>/</b></code> <code>{shr-server}/catchments/{catchment code}/encounters<code>
</summary>

##### Headers :

X-Auth-Token : {auth token returned from Identity Service Provider}<br>
client_id : {client id of requester in Identity Service Provider}<br>
From : {email_id of requester registered in Identity Service Provider}<br>
Accept: application/json(default) OR application/atom+xml<br>


</details>

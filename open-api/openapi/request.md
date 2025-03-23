# Request

#### 1. Request Endpoint URLs

<table><thead><tr><th>Environment</th><th>URL</th><th data-hidden></th></tr></thead><tbody><tr><td>Testing Environment</td><td><a href="https://backstage-b2b-pre.ufcfan.org">https://backstage-b2b-pre.ufcfan.org</a></td><td></td></tr><tr><td>Production Environment</td><td><a href="https://backend.blockatm.net">https://backend.blockatm.net</a></td><td></td></tr></tbody></table>



2. #### Request  Header

&#x20;Each server to server request needs to contain the following request headers.

<table><thead><tr><th width="212.0302734375">Parameter name</th><th width="375.4847412109375">Instructions</th><th>Example</th></tr></thead><tbody><tr><td>BlockATM-API-Key<br><mark style="color:red;"><strong>Required</strong></mark></td><td>You can easily find it at BlockATM console.</td><td>pk_payment_my3T68cbuIXf1x3QOEbWtFEfcJPxeBr8wTewDVM</td></tr><tr><td>BlockATM-Request-Time<br><mark style="color:red;"><strong>Required</strong></mark></td><td>The timing of your request, down to the millisecond.</td><td>1742725435000</td></tr><tr><td>BlockATM-Signature-V1</td><td>Signature using your serect key.</td><td></td></tr><tr><td>BlockATM-Rec_Window</td><td>The time window in milliseconds,<br>defaults to 30000 milliseconds if it is null.</td><td>30000 </td></tr></tbody></table>

When the server receives the request, it determines the timestamp in the request, and if it was made before 30000 milliseconds, the request is considered invalid. The time window value can be defined by sending the optional request header **BlockATM-RECV\_WINDOW**.



#### 3. Request **Parameters**

See the interface description



4.Response **Parameters**

| Parameter | Type     | Description                                                     |
| --------- | -------- | --------------------------------------------------------------- |
| code      | String   | system general return code. 200 -success, other exceptions      |
| success   | Boolean  | Marks whether the program processed successfully                |
| data      | Object   | Data body, unified return of each business response information |
| trace     | String   | Global link flag information                                    |
| msg       | String   | Some prompt messages processed by the program                   |






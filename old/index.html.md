---
title: Crew APIs v1.0.0
language_tabs:
  - ruby: Ruby
  - python: Python
  - curl: Curl
  - java: Java
  - javascript: " JavaScript"
  - go: Go
language_clients:
  - ruby: ""
  - python: ""
  - curl: ""
  - java: ""
  - javascript: ""
  - go: ""
toc_footers:
  - <a href="https://crewapp.com">Find out more about Crew</a>
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="crew-apis">Crew APIs v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

**Overview** <br /> The Crew APIs provide powerful capabilities to customize, automate, and integrate Crew. Important information and workflow can be pushed into Crew, and the APIs can also be used to gain visibility into activities happening within Crew. The below provides some common examples of ways the Crew APIs can be leveraged. In addition, Crew already provides [off-the-shelf integrations with these leading software providers](https://home.crewapp.com/integrations).<br /> <br /> **Getting Started**<br />To get started with the Crew APIs or for specific questions, please contact [developers@crewapp.com](mailto:developers@crewapp.com).<br /><br />**Common Use Cases**<br /><br />_Sync Scheduling Data with Crew_<br />Employees and teams benefit from having a single place to get all of the important information they need for a successful day at work. Integrating the team schedule with Crew means putting the schedule in every team member's pocket, in the same place they access all other critical work information. Crew APIs support two-way syncing of the scheduling, pushing scheduling data into Crew and syncing any changes to the schedule that happen within Crew (e.g., shift swaps and filling open shifts).<br /><br />_Push Important Information into Crew_<br />Getting the right information to your frontline teams can be a challenge. There's important information that lives in myriad systems. Crew APIs enable pushing the right information to the right team members at the right time. With the flexible Cards APIs, deliver beautifully formatted content that team members will engage with and can take action on from their mobile device.<br /><br />_Automate Tasks and Digitize Workflows_<br />Trying to reduce paper-based processes, copying information from one place to another, and other duplicative and wasted effort? Leverage Crew APIs to automate things like assigning tasks, collecting data, and notifying teams.<br /><br />_Sync Employee Roster with System of Record_<br />Crew syncs with any system of record to ensure that the employee roster and hierarchy in Crew mirrors the source of truth. Use Crew APIs to automatically onboard and remove employees from Crew.

Base URLs:

* <a href="https://api.crewapp.com/">https://api.crewapp.com/</a>

Email: <a href="mailto:developers@crewapp.com">Support</a> 

# Authentication

- oAuth2 authentication. Applications that integrate with Crew to take action on behalf of a Crew account must request permissions from the Crew account holder to perform those actions. OAuth is the mechanism applications use to request permissions from account holders. For information about OAuth specification, see [OAuth 2.0](https://oauth.net/2/).<br /><br />The following process is used to obtain permission from the Crew account holder in order to obtain Access Tokens to perform tasks on their behalf.<br /><br />**Appplication Provides Authorization Link**: Applications configure and serve a link with the following parameters:<br />+_scope_: A commma-separated list of the desired OAuth permissions<br />+_clientId_: Application's clientId<br />+_target_: Should always be ENTERPRISE_ACCOUNT<br />+_redirectUri_: The specific URI Crew should redirect back to<br />+_state_: (optional) Used by applicatin developer to prevent CSRF attacks<br /><br />**Account Holder Completes Permission Form**: After the Crew account holder clicks the authorization link, they are prompted with a permissions form hosted by Crew.<br /><br />**Crew Redirects with Authorization Code**: When the account holder clicks _Allow_ on the permission form, Crew sends an OAuth authorization code (as a URL parameter) to the redirect specified URL.<br /><br />**Application Exchanges for Access Token**: The client application uses the (short-lived) authorization code to request an OAuth access token from the /connect/oauth/access-token endpoint.

    - Flow: authorizationCode
    - Authorization URL = [https://crewapp.com/oauth/](https://crewapp.com/oauth/)
    - Token URL = [https://api.crewapp.com/connect/oauth/access-tokens](https://api.crewapp.com/connect/oauth/access-tokens)

|Scope|Scope Description|
|---|---|
|CALENDAR_VIEW|Grants read access to view calendar information|
|CALENDAR_EDIT|Grants write access to edit calendar information|
|ENTERPRISE_VIEW|Grants read access to view information about an enterprise|
|ORGANIZATION_MEMBER_VIEW|Grants read access to view information about an organization|
|MESSAGE_CONVERSATION|Grants permissions to send a message to a targeted conversation|
|MESSAGE_EVERYONE|Grants permissions to send a message to an everyone group, reaching all members of an organization|
|MIDDLEWARE_PUBLISH|Grants permission to publish location, user, and calendar items via the Crew middleware|

<h1 id="crew-apis-oauth">OAuth</h1>

Authenticate with our system

## To generate an Access Token

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.crewapp.com/connect/access-tokens',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('https://api.crewapp.com/connect/access-tokens', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/access-tokens");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript
const inputBody = '{
  "code": "string",
  "accessToken": null,
  "clientSecret": "string",
  "clientId": "string",
  "expirationTime": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('https://api.crewapp.com/connect/access-tokens',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api.crewapp.com/connect/access-tokens", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /connect/access-tokens`

All subsequent API calls to Crew require a valid Access Token. This call allows you to exchange a valid Authorization Code or renew a valid OAuth Token.

> Body parameter

```json
{
  "code": "string",
  "accessToken": null,
  "clientSecret": "string",
  "clientId": "string",
  "expirationTime": 0
}
```

<h3 id="to-generate-an-access-token-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[Access](#schemaaccess)|true|none|

> Example responses

> 200 Response

```json
[
  {
    "accessToken": "string",
    "expiresAt": 0,
    "acessTokenId": "string",
    "scope": [
      null
    ],
    "target": "string",
    "targetId": "string"
  }
]
```

<h3 id="to-generate-an-access-token-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|Inline|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<h3 id="to-generate-an-access-token-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» accessToken|string|false|none|Access token used to allow access to Crew's APIs|
|» expiresAt|integer|false|none|Epoch seconds of expiration date|
|» acessTokenId|string|false|none|Unique identifier|
|» scope|[any]|false|none|List of scopes the acess token has been granted|
|» target|string|false|none|The type of target -- e.g, ENTERPRISE_ACCOUNT -- the token is associated with|
|» targetId|string|false|none|The Crew ID of the target|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="crew-apis-users">Users</h1>

Retrieve User Information

## To fetch user information

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crewapp.com/connect/users/{userId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crewapp.com/connect/users/{userId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/users/{userId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/users/{userId}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://api.crewapp.com/connect/users/{userId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /connect/users/{userId}`

<h3 id="to-fetch-user-information-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|userId|path|integer(int64)|true|Id of user|

> Example responses

> 200 Response

```json
[
  {
    "id": "string",
    "profile": {
      "fullName": "string",
      "avatarPublicId": "string"
    }
  }
]
```

<h3 id="to-fetch-user-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|Inline|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<h3 id="to-fetch-user-information-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[UserResp](#schemauserresp)]|false|none|none|
|» id|string|false|none|Unique identifier for user|
|» profile|[UserProfile](#schemauserprofile)|false|none|none|
|»» fullName|string|false|none|Users full name|
|»» avatarPublicId|string|false|none|Unique identifier for users profile picture|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: ORGANIZATION_MEMBER_VIEW )
</aside>

<h1 id="crew-apis-organizations">Organizations</h1>

Get Information about an Organization

## To retrieve information about an organization

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crewapp.com/connect/organizations/{organizationId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crewapp.com/connect/organizations/{organizationId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/organizations/{organizationId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/organizations/{organizationId}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://api.crewapp.com/connect/organizations/{organizationId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /connect/organizations/{organizationId}`

<h3 id="to-retrieve-information-about-an-organization-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|organizationId|path|integer(int64)|true|Id of organization|

> Example responses

> 200 Response

```json
[
  {
    "organizationId": {
      "id": "string",
      "updatedAt": 0,
      "entityType": "string"
    }
  }
]
```

<h3 id="to-retrieve-information-about-an-organization-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful operation|Inline|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<h3 id="to-retrieve-information-about-an-organization-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[OrganizationResp](#schemaorganizationresp)]|false|none|none|
|» organizationId|[OrganizationId](#schemaorganizationid)|false|none|none|
|»» id|string|false|none|Unique identifier for organization|
|»» updatedAt|integer|false|none|Epoch milliseconds that the organization was last updated|
|»» entityType|string|false|none|ORGANIZATION|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: ORGANIZATION_MEMBER_VIEW )
</aside>

## To fetch organization members

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crewapp.com/connect/organizations/{organizationId}/members',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crewapp.com/connect/organizations/{organizationId}/members', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/organizations/{organizationId}/members");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/organizations/{organizationId}/members',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://api.crewapp.com/connect/organizations/{organizationId}/members", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /connect/organizations/{organizationId}/members`

<h3 id="to-fetch-organization-members-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|organizationId|path|integer(int64)|true|Id of organization|

> Example responses

> 200 Response

```json
[
  {
    "userId": {
      "id": "string",
      "updatedAt": 0,
      "entityType": "string"
    },
    "organizationId": {
      "id": "string",
      "updatedAt": 0,
      "entityType": "string"
    },
    "createdAt": 0,
    "updatedAt": 0,
    "permissions": {
      "admin": true
    },
    "profile": {
      "title": "string"
    }
  }
]
```

<h3 id="to-fetch-organization-members-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful operation|Inline|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<h3 id="to-fetch-organization-members-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[OrganizationMembershipResp](#schemaorganizationmembershipresp)]|false|none|none|
|» userId|[UserId](#schemauserid)|false|none|none|
|»» id|string|false|none|Unique identifier for user|
|»» updatedAt|integer|false|none|Epoch milliseconds that the user was last updated|
|»» entityType|string|false|none|USER|
|» organizationId|[OrganizationId](#schemaorganizationid)|false|none|none|
|»» id|string|false|none|Unique identifier for organization|
|»» updatedAt|integer|false|none|Epoch milliseconds that the organization was last updated|
|»» entityType|string|false|none|ORGANIZATION|
|» createdAt|integer|false|none|Epoch milliseconds that the membership was created at|
|» updatedAt|integer|false|none|Epoch milliseconds that the membership was last updated at|
|» permissions|[Permissions](#schemapermissions)|false|none|none|
|»» admin|boolean|false|none|whether user is an organization admin or not|
|» profile|[Profile](#schemaprofile)|false|none|none|
|»» title|string|false|none|Employees title|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: ORGANIZATION_MEMBER_VIEW )
</aside>

<h1 id="crew-apis-enterprises">Enterprises</h1>

Get Information About on an Enterprise

## To retrieve information about an enterprise

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crewapp.com/connect/enterprises/{enterpriseId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crewapp.com/connect/enterprises/{enterpriseId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/enterprises/{enterpriseId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/enterprises/{enterpriseId}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://api.crewapp.com/connect/enterprises/{enterpriseId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /connect/enterprises/{enterpriseId}`

<h3 id="to-retrieve-information-about-an-enterprise-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|enterpriseId|path|integer(int64)|true|Id of enterprise|

> Example responses

> 200 Response

```json
[
  {
    "organizationId": {
      "id": "string",
      "updatedAt": 0,
      "entityType": "string"
    }
  }
]
```

<h3 id="to-retrieve-information-about-an-enterprise-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful operation|Inline|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<h3 id="to-retrieve-information-about-an-enterprise-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[EnterpriseResp](#schemaenterpriseresp)]|false|none|none|
|» organizationId|[EnterpriseId](#schemaenterpriseid)|false|none|none|
|»» id|string|false|none|Unique identifier for enterprise|
|»» updatedAt|integer|false|none|Epoch milliseconds that the enterprise was last updated|
|»» entityType|string|false|none|ENTERPRISE|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: ENTERPRISE_VIEW )
</aside>

## To get a list of the organizations within an enterprise

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crewapp.com/connect/enterprises/{enterpriseId}/organizations',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crewapp.com/connect/enterprises/{enterpriseId}/organizations', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/enterprises/{enterpriseId}/organizations");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/enterprises/{enterpriseId}/organizations',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://api.crewapp.com/connect/enterprises/{enterpriseId}/organizations", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /connect/enterprises/{enterpriseId}/organizations`

<h3 id="to-get-a-list-of-the-organizations-within-an-enterprise-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|enterpriseId|path|integer(int64)|true|Id of enterprise|

> Example responses

> 200 Response

```json
[
  {
    "organizationId": {
      "id": "string",
      "updatedAt": 0,
      "entityType": "string"
    },
    "updatedAt": null
  }
]
```

<h3 id="to-get-a-list-of-the-organizations-within-an-enterprise-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|successful operation|Inline|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<h3 id="to-get-a-list-of-the-organizations-within-an-enterprise-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[EnterpriseOrgsResp](#schemaenterpriseorgsresp)]|false|none|none|
|» organizationId|[OrganizationId](#schemaorganizationid)|false|none|none|
|»» id|string|false|none|Unique identifier for organization|
|»» updatedAt|integer|false|none|Epoch milliseconds that the organization was last updated|
|»» entityType|string|false|none|ORGANIZATION|
|» updatedAt|any|false|none|Epoch milliseconds that the organization membership was last updated|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: ENTERPRISE_VIEW )
</aside>

<h1 id="crew-apis-calendar-items">Calendar Items</h1>

Create & Update Shifts and Other Calendar Items

## Creates calendar item with the specified parameters

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'https://api.crewapp.com/connect/calendar-items',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crewapp.com/connect/calendar-items', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/calendar-items");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript
const inputBody = '{
  "organizationId": "string",
  "start": 0,
  "end": 0,
  "timeZoneName": "string",
  "type": "TIME_OFF",
  "notes": "string",
  "muteAssignmentNotifications": true,
  "members": {
    "type": "USER",
    "userId": "string"
  },
  "name": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/calendar-items',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api.crewapp.com/connect/calendar-items", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /connect/calendar-items`

> Body parameter

```json
{
  "organizationId": "string",
  "start": 0,
  "end": 0,
  "timeZoneName": "string",
  "type": "TIME_OFF",
  "notes": "string",
  "muteAssignmentNotifications": true,
  "members": {
    "type": "USER",
    "userId": "string"
  },
  "name": "string"
}
```

<h3 id="creates-calendar-item-with-the-specified-parameters-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[CalendarItems](#schemacalendaritems)|true|none|

<h3 id="creates-calendar-item-with-the-specified-parameters-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_EDIT )
</aside>

## To fetch calendar items for given time range

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crewapp.com/connect/organizations/{organizationId}/calendar-items',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crewapp.com/connect/organizations/{organizationId}/calendar-items', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/organizations/{organizationId}/calendar-items");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/organizations/{organizationId}/calendar-items',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://api.crewapp.com/connect/organizations/{organizationId}/calendar-items", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /connect/organizations/{organizationId}/calendar-items`

<h3 id="to-fetch-calendar-items-for-given-time-range-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|organizationId|path|integer(int64)|true|Id of organization|
|startsAtOrAfter|query|string|false|Epoch time in milliseconds that calendar item starts after|
|startsAtOrBefore|query|string|false|Epoch time in milliseconds that calendar item starts before|

<h3 id="to-fetch-calendar-items-for-given-time-range-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_VIEW )
</aside>

## To fetch calendar item by passed ID

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crewapp.com/connect/calendar-items/{calendarItemId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crewapp.com/connect/calendar-items/{calendarItemId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/calendar-items/{calendarItemId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://api.crewapp.com/connect/calendar-items/{calendarItemId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /connect/calendar-items/{calendarItemId}`

<h3 id="to-fetch-calendar-item-by-passed-id-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|calendarItemId|path|integer|true|Id of calendar item|

<h3 id="to-fetch-calendar-item-by-passed-id-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_VIEW )
</aside>

## Updates calendar item with passed parameters

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.patch 'https://api.crewapp.com/connect/calendar-items/{calendarItemId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.patch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/calendar-items/{calendarItemId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PATCH");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript
const inputBody = '{
  "notes": "string",
  "start": "string",
  "end": "string",
  "status": "string",
  "muteAssignmentNotifications": true,
  "name": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}',
{
  method: 'PATCH',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PATCH", "https://api.crewapp.com/connect/calendar-items/{calendarItemId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PATCH /connect/calendar-items/{calendarItemId}`

Any explicit JSON null values or empty strings will be interpreted as an unset

> Body parameter

```json
{
  "notes": "string",
  "start": "string",
  "end": "string",
  "status": "string",
  "muteAssignmentNotifications": true,
  "name": "string"
}
```

<h3 id="updates-calendar-item-with-passed-parameters-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|calendarItemId|path|integer(int64)|true|Id of calendar item|
|body|body|[PatchCalendarItems](#schemapatchcalendaritems)|true|none|

<h3 id="updates-calendar-item-with-passed-parameters-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_EDIT )
</aside>

## Mark the calendar item with the given id deleted

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.delete 'https://api.crewapp.com/connect/calendar-items/{calendarItemId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.delete('https://api.crewapp.com/connect/calendar-items/{calendarItemId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/calendar-items/{calendarItemId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://api.crewapp.com/connect/calendar-items/{calendarItemId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /connect/calendar-items/{calendarItemId}`

<h3 id="mark-the-calendar-item-with-the-given-id-deleted-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|calendarItemId|path|integer(int64)|true|Id of calendar item|

<h3 id="mark-the-calendar-item-with-the-given-id-deleted-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_EDIT )
</aside>

<h1 id="crew-apis-calendar-item-members">Calendar Item Members</h1>

Assign/Remove Users to Existing Calendar Items

## To add new assignees

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript
const inputBody = '{
  "newCalendarItemStatus": "OPEN",
  "shouldReplaceMemberStatuses": true,
  "members": {
    "type": "INVITE",
    "userId": "string",
    "groupId": "string",
    "fullName": "string",
    "countryCode": "string",
    "phone": "string",
    "initialStatus": "ACCEPTED"
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /connect/calendar-items/{calendarItemId}/members`

> Body parameter

```json
{
  "newCalendarItemStatus": "OPEN",
  "shouldReplaceMemberStatuses": true,
  "members": {
    "type": "INVITE",
    "userId": "string",
    "groupId": "string",
    "fullName": "string",
    "countryCode": "string",
    "phone": "string",
    "initialStatus": "ACCEPTED"
  }
}
```

<h3 id="to-add-new-assignees-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|calendarItemId|path|integer(int64)|true|Id of calendar item|
|body|body|[CalendarItemsMembers](#schemacalendaritemsmembers)|true|none|

<h3 id="to-add-new-assignees-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_EDIT )
</aside>

## For a user to request a shift if you aren’t part of it already

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript
const inputBody = '{
  "status": "ADDITION_REQUESTED"
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /connect/calendar-items/{calendarItemId}/members/{userId}`

> Body parameter

```json
{
  "status": "ADDITION_REQUESTED"
}
```

<h3 id="for-a-user-to-request-a-shift-if-you-aren’t-part-of-it-already-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|calendarItemId|path|integer(int64)|true|Id of calendar item|
|userId|path|integer(int64)|true|Id of user|
|body|body|[AdditionRequested](#schemaadditionrequested)|true|order placed for purchasing the pet|

<h3 id="for-a-user-to-request-a-shift-if-you-aren’t-part-of-it-already-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_EDIT )
</aside>

## To approve a cover

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.patch 'https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.patch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PATCH");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript
const inputBody = '{
  "status": "ACCEPTED"
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}',
{
  method: 'PATCH',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PATCH", "https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PATCH /connect/calendar-items/{calendarItemId}/members/{userId}`

> Body parameter

```json
{
  "status": "ACCEPTED"
}
```

<h3 id="to-approve-a-cover-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|calendarItemId|path|integer(int64)|true|Id of calendar item|
|userId|path|integer(int64)|true|Id of user|
|body|body|[Status](#schemastatus)|true|order placed for purchasing the pet|

<h3 id="to-approve-a-cover-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_EDIT )
</aside>

## To remove a user from a shift

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.delete 'https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.delete('https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://api.crewapp.com/connect/calendar-items/{calendarItemId}/members/{userId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /connect/calendar-items/{calendarItemId}/members/{userId}`

<h3 id="to-remove-a-user-from-a-shift-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|calendarItemId|path|integer(int64)|true|Id of calendar item|
|userId|path|integer(int64)|true|Id of the user|

<h3 id="to-remove-a-user-from-a-shift-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: CALENDAR_EDIT )
</aside>

<h1 id="crew-apis-cards">Cards</h1>

Generate Formatted HTML 'Cards'

## To create a new card

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'https://api.crewapp.com/connect/cards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crewapp.com/connect/cards', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/cards");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript
const inputBody = '{
  "templateId": "string",
  "content": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/cards',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api.crewapp.com/connect/cards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /connect/cards`

> Body parameter

```json
{
  "templateId": "string",
  "content": "string"
}
```

<h3 id="to-create-a-new-card-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[CardInput](#schemacardinput)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string"
}
```

<h3 id="to-create-a-new-card-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|[CardResp](#schemacardresp)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: MESSAGE_CONVERSATION )
</aside>

<h1 id="crew-apis-messages">Messages</h1>

Send Messages into Crew

## To send messages into Crew

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post 'https://api.crewapp.com/connect/messages',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('https://api.crewapp.com/connect/messages', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/connect/messages");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript
const inputBody = '{
  "cardId": "string",
  "organizationId": "string",
  "conversationId": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/connect/messages',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://api.crewapp.com/connect/messages", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /connect/messages`

> Body parameter

```json
{
  "cardId": "string",
  "organizationId": "string",
  "conversationId": "string"
}
```

<h3 id="to-send-messages-into-crew-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[MessageInput](#schemamessageinput)|true|none|

> Example responses

> 200 Response

```json
{
  "id": "string"
}
```

<h3 id="to-send-messages-into-crew-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|[MessageResp](#schemamessageresp)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: MESSAGE_CONVERSATION )
</aside>

<h1 id="crew-apis-assets">Assets</h1>

Retrieve User Assets

## to fetch image assets corresponding to users profile picture

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get 'https://api.crewapp.com/assets/{publicId}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('https://api.crewapp.com/assets/{publicId}', headers = headers)

print(r.json())

```

```java
URL obj = new URL("https://api.crewapp.com/assets/{publicId}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```javascript

const headers = {
  'Authorization':'Bearer {access-token}'
};

fetch('https://api.crewapp.com/assets/{publicId}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://api.crewapp.com/assets/{publicId}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /assets/{publicId}`

<h3 id="to-fetch-image-assets-corresponding-to-users-profile-picture-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|publicId|path|integer(int64)|true|Public Id|

<h3 id="to-fetch-image-assets-corresponding-to-users-profile-picture-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful operation|None|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|Invalid input|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
crew_auth ( Scopes: ORGANIZATION_MEMBER_VIEW )
</aside>

# Schemas

<h2 id="tocS_Access">Access</h2>
<!-- backwards compatibility -->
<a id="schemaaccess"></a>
<a id="schema_Access"></a>
<a id="tocSaccess"></a>
<a id="tocsaccess"></a>

```json
{
  "code": "string",
  "accessToken": null,
  "clientSecret": "string",
  "clientId": "string",
  "expirationTime": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|code|string|false|none|An Authorization Code that can be exchanged for an Access Token as long as the code is still valid|
|accessToken|any|false|none|An Access Token that can be exchanged for a new Access Token as long as the exisitng token is still valid|
|clientSecret|string|false|none|Application secret provided by Crew|
|clientId|string|true|none|Application Client Id|
|expirationTime|integer|false|none|Epoch time in seconds that token is desired to expire at. If not passed the token will default to being good for 30 days. Tokens cannot have an expiration more than 90 days in the future|

<h2 id="tocS_AdditionRequested">AdditionRequested</h2>
<!-- backwards compatibility -->
<a id="schemaadditionrequested"></a>
<a id="schema_AdditionRequested"></a>
<a id="tocSadditionrequested"></a>
<a id="tocsadditionrequested"></a>

```json
{
  "status": "ADDITION_REQUESTED"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|string|false|none|ADDITION_REQUESTED|

<h2 id="tocS_Status">Status</h2>
<!-- backwards compatibility -->
<a id="schemastatus"></a>
<a id="schema_Status"></a>
<a id="tocSstatus"></a>
<a id="tocsstatus"></a>

```json
{
  "status": "ACCEPTED"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|string|false|none|ACCEPTED, DECLINED|

#### Enumerated Values

|Property|Value|
|---|---|
|status|ACCEPTED|
|status|DECLINED|

<h2 id="tocS_PatchCalendarItems">PatchCalendarItems</h2>
<!-- backwards compatibility -->
<a id="schemapatchcalendaritems"></a>
<a id="schema_PatchCalendarItems"></a>
<a id="tocSpatchcalendaritems"></a>
<a id="tocspatchcalendaritems"></a>

```json
{
  "notes": "string",
  "start": "string",
  "end": "string",
  "status": "string",
  "muteAssignmentNotifications": true,
  "name": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|notes|string|false|none|Text description for the calendar item|
|start|string|false|none|Time in millis since epoch for start of shift|
|end|string|false|none|Time in millis since epoch for end of shift|
|status|string|false|none|Status for the calendar item|
|muteAssignmentNotifications|boolean|false|none|Specifies whether notification for assignment should be muted or not|
|name|string|false|none|Name of associated with the calendar item|

<h2 id="tocS_CalendarItems">CalendarItems</h2>
<!-- backwards compatibility -->
<a id="schemacalendaritems"></a>
<a id="schema_CalendarItems"></a>
<a id="tocScalendaritems"></a>
<a id="tocscalendaritems"></a>

```json
{
  "organizationId": "string",
  "start": 0,
  "end": 0,
  "timeZoneName": "string",
  "type": "TIME_OFF",
  "notes": "string",
  "muteAssignmentNotifications": true,
  "members": {
    "type": "USER",
    "userId": "string"
  },
  "name": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|organizationId|string|true|none|Organization that calendar item belongs to|
|start|integer|true|none|Time in millis since epoch for start of shift|
|end|integer|true|none|Time in millis since epoch for end of shift|
|timeZoneName|string|true|none|Time zone where shift was created|
|type|string|true|none|Possible values: TIME_OFF, MEETING, MULTI_ASSIGNEE_SHIFT|
|notes|string|false|none|Text description for the calendar item|
|muteAssignmentNotifications|boolean|false|none|specifies whether notification for assignment should be muted or not|
|members|[Members](#schemamembers)|false|none|none|
|name|string|false|none|Display name for the calendar item|

#### Enumerated Values

|Property|Value|
|---|---|
|type|TIME_OFF|
|type|MEETING|
|type|MULTI_ASSIGNEE_SHIFT|

<h2 id="tocS_CalendarItemsMembers">CalendarItemsMembers</h2>
<!-- backwards compatibility -->
<a id="schemacalendaritemsmembers"></a>
<a id="schema_CalendarItemsMembers"></a>
<a id="tocScalendaritemsmembers"></a>
<a id="tocscalendaritemsmembers"></a>

```json
{
  "newCalendarItemStatus": "OPEN",
  "shouldReplaceMemberStatuses": true,
  "members": {
    "type": "INVITE",
    "userId": "string",
    "groupId": "string",
    "fullName": "string",
    "countryCode": "string",
    "phone": "string",
    "initialStatus": "ACCEPTED"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|newCalendarItemStatus|string|true|none|OPEN, ASSIGNED (or any other CalendarItemStatus)|
|shouldReplaceMemberStatuses|boolean|true|none|If true, member statuses will be replaced. Otherwise, existing member statuses will not be replaced|
|members|[CalendarMembers](#schemacalendarmembers)|true|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|newCalendarItemStatus|OPEN|
|newCalendarItemStatus|ASSIGNED|

<h2 id="tocS_CalendarMembers">CalendarMembers</h2>
<!-- backwards compatibility -->
<a id="schemacalendarmembers"></a>
<a id="schema_CalendarMembers"></a>
<a id="tocScalendarmembers"></a>
<a id="tocscalendarmembers"></a>

```json
{
  "type": "INVITE",
  "userId": "string",
  "groupId": "string",
  "fullName": "string",
  "countryCode": "string",
  "phone": "string",
  "initialStatus": "ACCEPTED"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|true|none|ENUM - INVITE, USER, GROUP|
|userId|string|false|none|Unique id for user|
|groupId|string|false|none|Unique id for group|
|fullName|string|false|none|Name for user if invite|
|countryCode|string|false|none|Numeric country code for phone number|
|phone|string|false|none|Phone number|
|initialStatus|string|true|none|ACCEPTED, ASSIGNED, PENDING_RESPONSE, DECLINED, DELETED, ADDITION_REQUESTED, REPLACEMENT_REQUESTED, DENIED|

#### Enumerated Values

|Property|Value|
|---|---|
|type|INVITE|
|type|USER|
|type|GROUP|
|initialStatus|ACCEPTED|
|initialStatus|ASSIGNED|
|initialStatus|PENDING_RESPONSE|
|initialStatus|DECLINED|
|initialStatus|DELETED|
|initialStatus|ADDITION_REQUESTED|
|initialStatus|REPLACEMENT_REQUESTED|
|initialStatus|DENIED|

<h2 id="tocS_Members">Members</h2>
<!-- backwards compatibility -->
<a id="schemamembers"></a>
<a id="schema_Members"></a>
<a id="tocSmembers"></a>
<a id="tocsmembers"></a>

```json
{
  "type": "USER",
  "userId": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|false|none|ENUM - USER|
|userId|string|false|none|Unique id for user|

#### Enumerated Values

|Property|Value|
|---|---|
|type|USER|

<h2 id="tocS_AccessResp">AccessResp</h2>
<!-- backwards compatibility -->
<a id="schemaaccessresp"></a>
<a id="schema_AccessResp"></a>
<a id="tocSaccessresp"></a>
<a id="tocsaccessresp"></a>

```json
{
  "accessToken": "string",
  "expiresAt": 0,
  "acessTokenId": "string",
  "scope": [
    null
  ],
  "target": "string",
  "targetId": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|accessToken|string|false|none|Access token used to allow access to Crew's APIs|
|expiresAt|integer|false|none|Epoch seconds of expiration date|
|acessTokenId|string|false|none|Unique identifier|
|scope|[any]|false|none|List of scopes the acess token has been granted|
|target|string|false|none|The type of target -- e.g, ENTERPRISE_ACCOUNT -- the token is associated with|
|targetId|string|false|none|The Crew ID of the target|

<h2 id="tocS_OrganizationResp">OrganizationResp</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationresp"></a>
<a id="schema_OrganizationResp"></a>
<a id="tocSorganizationresp"></a>
<a id="tocsorganizationresp"></a>

```json
{
  "organizationId": {
    "id": "string",
    "updatedAt": 0,
    "entityType": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|organizationId|[OrganizationId](#schemaorganizationid)|false|none|none|

<h2 id="tocS_OrganizationMembershipResp">OrganizationMembershipResp</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationmembershipresp"></a>
<a id="schema_OrganizationMembershipResp"></a>
<a id="tocSorganizationmembershipresp"></a>
<a id="tocsorganizationmembershipresp"></a>

```json
{
  "userId": {
    "id": "string",
    "updatedAt": 0,
    "entityType": "string"
  },
  "organizationId": {
    "id": "string",
    "updatedAt": 0,
    "entityType": "string"
  },
  "createdAt": 0,
  "updatedAt": 0,
  "permissions": {
    "admin": true
  },
  "profile": {
    "title": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|userId|[UserId](#schemauserid)|false|none|none|
|organizationId|[OrganizationId](#schemaorganizationid)|false|none|none|
|createdAt|integer|false|none|Epoch milliseconds that the membership was created at|
|updatedAt|integer|false|none|Epoch milliseconds that the membership was last updated at|
|permissions|[Permissions](#schemapermissions)|false|none|none|
|profile|[Profile](#schemaprofile)|false|none|none|

<h2 id="tocS_EnterpriseResp">EnterpriseResp</h2>
<!-- backwards compatibility -->
<a id="schemaenterpriseresp"></a>
<a id="schema_EnterpriseResp"></a>
<a id="tocSenterpriseresp"></a>
<a id="tocsenterpriseresp"></a>

```json
{
  "organizationId": {
    "id": "string",
    "updatedAt": 0,
    "entityType": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|organizationId|[EnterpriseId](#schemaenterpriseid)|false|none|none|

<h2 id="tocS_EnterpriseOrgsResp">EnterpriseOrgsResp</h2>
<!-- backwards compatibility -->
<a id="schemaenterpriseorgsresp"></a>
<a id="schema_EnterpriseOrgsResp"></a>
<a id="tocSenterpriseorgsresp"></a>
<a id="tocsenterpriseorgsresp"></a>

```json
{
  "organizationId": {
    "id": "string",
    "updatedAt": 0,
    "entityType": "string"
  },
  "updatedAt": null
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|organizationId|[OrganizationId](#schemaorganizationid)|false|none|none|
|updatedAt|any|false|none|Epoch milliseconds that the organization membership was last updated|

<h2 id="tocS_UserId">UserId</h2>
<!-- backwards compatibility -->
<a id="schemauserid"></a>
<a id="schema_UserId"></a>
<a id="tocSuserid"></a>
<a id="tocsuserid"></a>

```json
{
  "id": "string",
  "updatedAt": 0,
  "entityType": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Unique identifier for user|
|updatedAt|integer|false|none|Epoch milliseconds that the user was last updated|
|entityType|string|false|none|USER|

<h2 id="tocS_OrganizationId">OrganizationId</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationid"></a>
<a id="schema_OrganizationId"></a>
<a id="tocSorganizationid"></a>
<a id="tocsorganizationid"></a>

```json
{
  "id": "string",
  "updatedAt": 0,
  "entityType": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Unique identifier for organization|
|updatedAt|integer|false|none|Epoch milliseconds that the organization was last updated|
|entityType|string|false|none|ORGANIZATION|

<h2 id="tocS_EnterpriseId">EnterpriseId</h2>
<!-- backwards compatibility -->
<a id="schemaenterpriseid"></a>
<a id="schema_EnterpriseId"></a>
<a id="tocSenterpriseid"></a>
<a id="tocsenterpriseid"></a>

```json
{
  "id": "string",
  "updatedAt": 0,
  "entityType": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Unique identifier for enterprise|
|updatedAt|integer|false|none|Epoch milliseconds that the enterprise was last updated|
|entityType|string|false|none|ENTERPRISE|

<h2 id="tocS_Permissions">Permissions</h2>
<!-- backwards compatibility -->
<a id="schemapermissions"></a>
<a id="schema_Permissions"></a>
<a id="tocSpermissions"></a>
<a id="tocspermissions"></a>

```json
{
  "admin": true
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|admin|boolean|false|none|whether user is an organization admin or not|

<h2 id="tocS_Profile">Profile</h2>
<!-- backwards compatibility -->
<a id="schemaprofile"></a>
<a id="schema_Profile"></a>
<a id="tocSprofile"></a>
<a id="tocsprofile"></a>

```json
{
  "title": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|title|string|false|none|Employees title|

<h2 id="tocS_UserResp">UserResp</h2>
<!-- backwards compatibility -->
<a id="schemauserresp"></a>
<a id="schema_UserResp"></a>
<a id="tocSuserresp"></a>
<a id="tocsuserresp"></a>

```json
{
  "id": "string",
  "profile": {
    "fullName": "string",
    "avatarPublicId": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Unique identifier for user|
|profile|[UserProfile](#schemauserprofile)|false|none|none|

<h2 id="tocS_UserProfile">UserProfile</h2>
<!-- backwards compatibility -->
<a id="schemauserprofile"></a>
<a id="schema_UserProfile"></a>
<a id="tocSuserprofile"></a>
<a id="tocsuserprofile"></a>

```json
{
  "fullName": "string",
  "avatarPublicId": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fullName|string|false|none|Users full name|
|avatarPublicId|string|false|none|Unique identifier for users profile picture|

<h2 id="tocS_CardInput">CardInput</h2>
<!-- backwards compatibility -->
<a id="schemacardinput"></a>
<a id="schema_CardInput"></a>
<a id="tocScardinput"></a>
<a id="tocscardinput"></a>

```json
{
  "templateId": "string",
  "content": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|templateId|string|false|none|Template ID for card provided by Crew|
|content|string|false|none|Key value pairs that will fill in parts of the card. The supported values and what part of the card they effect will be communicated as designs are finalized|

<h2 id="tocS_CardResp">CardResp</h2>
<!-- backwards compatibility -->
<a id="schemacardresp"></a>
<a id="schema_CardResp"></a>
<a id="tocScardresp"></a>
<a id="tocscardresp"></a>

```json
{
  "id": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|ID of the resultant card|

<h2 id="tocS_MessageInput">MessageInput</h2>
<!-- backwards compatibility -->
<a id="schemamessageinput"></a>
<a id="schema_MessageInput"></a>
<a id="tocSmessageinput"></a>
<a id="tocsmessageinput"></a>

```json
{
  "cardId": "string",
  "organizationId": "string",
  "conversationId": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|cardId|string|false|none|ID of the card being sent in the message|
|organizationId|string|false|none|ID of the organization|
|conversationId|string|false|none|ID of the conversation|

<h2 id="tocS_MessageResp">MessageResp</h2>
<!-- backwards compatibility -->
<a id="schemamessageresp"></a>
<a id="schema_MessageResp"></a>
<a id="tocSmessageresp"></a>
<a id="tocsmessageresp"></a>

```json
{
  "id": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|ID of the message|


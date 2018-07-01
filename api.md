## Entrypoint
#### match
* `GET` `/`
#### policies
* **inbound**
    * validate-jwt, not required
    * response
        * body:
            * version: ???
            * no token: authenticate & register
            * valid token: refreshToken & account
        * statusCode: 200
        * contentType: `application/vnd.djchampionship.entrypoint+json;version=1`
* **outbound**
    * hydra

## Tokens
#### policies
* **match**
    * `POST` `/connect/token`
* **backend**
    * forward: `identity-service`

## Account
#### match
* `GET` `/accounts/{userName}`
* `POST` `/accounts`
#### policies
* **inbound**
    * validate-jwt, required
* **backend**
    * forward: `account-service`
* **outbound**
    * hydra

## PartyManagement
#### match
* `GET` `/musicproviders`
* `GET` `/musicproviders/{id}`
* `GET` `/parties?partyName={partyName}&partySecret={partySecret}`
* `GET` `/parties/{partyToken}`
* `GET` `/accounts/{userName}/parties`
* `POST` `/parties`
#### policies
* **inbound**
    * validate-jwt, required
* **backend**
    * forward: `party-management-service`
* **outbound**
    * hydra





# Channel-to-Bot Authentication and Authorization

In order for Channels and Bots built using the Bot Framework SDK to communicate with each other securely, the framework implements OAuth 2.0 authorization flows with [OpenID Connect](https://openid.net/connect/) authentication. For a Channel to send activities to a Bot, the Bot must receive a Token, detailing that the Channel is authorized to send activites to the Bot.

```mermaid
    graph LR
        Channel -- Token --> Bot(Bot)
```

When using the Bot Framework SDK and the default `BotFrameworkAdapter` (i.e. not a custom adapter), the Activity flow includes the Connector layer in between the Channel and Bot. The Connector is part of Azure Bot Service in the cloud, that allows Bots to exhange messages with multiple Channels configured through the Azure portal.

```mermaid
    graph LR
        Teams --- Connector
        Slack --- Connector([Connector])
        Cortana --- Connector
        WebChat --- Connector

        Connector --- Bot(Bot)
```
___

## Scenario: User Sends a Message from Channel to Bot

*User at Channel sends message to Bot*
```mermaid
    graph LR
        Channel -- "#quot;Why hello, Bot!#quot;" --> Bot(Bot)
```
OAuth participants in this scenario:
- **Channel**: OAuth Client
- **Connector**: Authorization Server (AS) or Identity Provider (IdP)
- **Bot**: Protected Resource or the external service the client is trying to access

For more information on OAuth fundamentals regarding what exactly the components in OAuth flows are, see [Azure Active Directory V2 Protocols documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-protocols).

Depending on the request scenario, the User or the Channel itself first authenticates to the authorization endpoint of the Connector (`"/oauth2/v2.0/authorize"`), then authorizes the Channel to send messages to the Bot. As part of this process, to ensure the security of this authorization, the Connector, following [OpenID Connect](https://openid.net/connect/) standards, implements [JSON Object Signing and Encryption](https://www.iana.org/assignments/jose/jose.xhtml) (JOSE) specifications. After the Channel authenticates and authorizes at the Connector, the Connector creates an access token and identity token, [asymmetrically signing](https://openid.net/specs/openid-connect-core-1_0.html#Signing) both.

*Channel Acting on Behalf of Itself*
```mermaid
    sequenceDiagram
        participant Channel
        participant Connector
        participant Bot

        Channel ->> Connector: authenticates and authorizes itself
        Connector ->> Connector: creates and signs access and identity tokens
        Connector ->> Channel: returns access and identity tokens
        Channel ->> Connector: makes request with access token to send message
        Connector ->> Bot: sends "Why hello, Bot!" with access token

```

*Channel Activing on Behalf of User*
```mermaid
    sequenceDiagram
        participant User
        participant Channel
        participant Connector
        participant Bot

        User ->> Channel: send "Why hello, Bot!" to Bot
        Channel ->> User: requests authorization
        User ->> Connector: authenticates and authorizes Channel
        Connector ->> Connector: creates and signs access and identity tokens
        Connector ->> Channel: returns access and identity tokens
        Channel ->> Connector: makes request with access token to send message
        Connector ->> Bot: sends "Why hello, Bot!" with access token
```

The Channel's request hits the Bot's `"api/messages"` endpoint, where the SDK verifies the validity of the Token before allowing the request to process with the Bot's business logic. 
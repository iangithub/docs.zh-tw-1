---
title: <issuedTokenParameters>
ms.date: 03/30/2017
ms.assetid: 120b3f37-7331-4816-b712-d6aab39655a4
ms.openlocfilehash: 6bdf56e3d2084dec8d44e1c4d3f0c1e50b711b92
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "61758233"
---
# <a name="issuedtokenparameters"></a>\<issuedTokenParameters>
指定在聯合安全性案例中發行之安全性權杖的參數。  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<binding>  
\<安全性 >  
\<issuedTokenParameters>  
  
## <a name="syntax"></a>語法  
  
```xml  
<issuedTokenParameters defaultMessageSecurityVersion="System.ServiceModel.MessageSecurityVersion"
                       inclusionMode="AlwaysToInitiator/AlwaysToRecipient/Never/Once"
                       keySize="Integer"
                       keyType="AsymmetricKey/BearerKey/SymmetricKey"
                       tokenType="String">
  <additionalRequestParameters />
  <claimTypeRequirements>
    <add claimType="URI"
         isOptional="Boolean" />
  </claimTypeRequirements>
  <issuer address="String"
          binding="" />
  <issuerMetadata address="String" />
</issuedTokenParameters>
```  
  
## <a name="type"></a>類型  
 `Type`  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列各節描述屬性、子項目和父項目。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|defaultMessageSecurityVersion|指定繫結必須支援的安全性規格版本 (WS-Security、WS-Trust、WS-Secure Conversation 和 WS-Security Policy)。 這個值的型別為 <xref:System.ServiceModel.MessageSecurityVersion>。|  
|inclusionMode|指定權杖內含需求。 此屬性的型別為 <xref:System.ServiceModel.Security.Tokens.SecurityTokenInclusionMode>。|  
|keySize|指定權杖金鑰大小的整數。 預設值為 256。|  
|keyType|指定金鑰型別之 <xref:System.IdentityModel.Tokens.SecurityKeyType> 的有效值。 預設為 `SymmetricKey`。|  
|tokenType|指定權杖型別的字串。 預設值為 "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAML"。|  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<additionalRequestParameters>](../../../../../docs/framework/configure-apps/file-schema/wcf/additionalrequestparameters-element.md)|指定額外要求參數的組態項目集合。|  
|[\<claimTypeRequirements>](../../../../../docs/framework/configure-apps/file-schema/wcf/claimtyperequirements-element.md)|指定必要宣告型別的集合。<br /><br /> 在聯合案例中，服務會聲明對傳入認證的需求。 例如，傳入認證必須處理特定的一組宣告型別。 這個集合中的每一個項目都會指定要顯示在聯合認證中的必要和選擇性宣告型別。|  
|[\<issuer>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuer-of-issuedtokenparameters.md)|指定發行目前權杖之端點的組態項目。|  
|[\<issuerMetadata>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuermetadata-of-issuedtokenparameters.md)|指定權杖簽發者中繼資料之端點位址的組態項目。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<secureConversationBootstrap>](../../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)|指定用於啟始安全對話服務的預設值。|  
|[\<security>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)|指定自訂繫結的安全性選項。|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>
- <xref:System.ServiceModel.Configuration.IssuedTokenParametersElement>
- <xref:System.ServiceModel.Configuration.SecurityElementBase.IssuedTokenParameters%2A>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [繫結](../../../../../docs/framework/wcf/bindings.md)
- [擴充繫結](../../../../../docs/framework/wcf/extending/extending-bindings.md)
- [自訂繫結](../../../../../docs/framework/wcf/extending/custom-bindings.md)
- [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)
- [如何：建立自訂繫結使用 SecurityBindingElement](../../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [自訂繫結安全性](../../../../../docs/framework/wcf/samples/custom-binding-security.md)
- [服務身分識別和驗證](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [同盟與發行的權杖](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)
- [自訂繫結的安全性功能](../../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)
- [同盟與發行的權杖](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)

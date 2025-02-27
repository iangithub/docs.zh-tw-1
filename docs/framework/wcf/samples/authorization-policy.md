---
title: 授權原則
ms.date: 03/30/2017
ms.assetid: 1db325ec-85be-47d0-8b6e-3ba2fdf3dda0
ms.openlocfilehash: f148af25f85731c4ff15727b328f3f905356fe6e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637462"
---
# <a name="authorization-policy"></a>授權原則

此範例示範如何實作自訂宣告授權原則以及關聯的自訂服務授權管理員。 當服務對服務作業執行宣告架構的存取檢查，以及在執行存取檢查前便授予呼叫者特定權限時，這個方法就會很有用處。 此範例同時說明新增宣告的處理序，以及對最後宣告集的存取檢查處理序。 用戶端與伺服器之間的所有應用程式訊息都會經過簽署及加密。 根據預設，使用 `wsHttpBinding` 繫結時，會使用用戶端所提供的使用者名稱和密碼來登入有效的 Windows NT 帳戶。 此範例示範如何使用自訂 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> 來驗證用戶端。 此外，此範例會說明用戶端如何使用 X.509 憑證來向服務進行驗證。 此範例說明 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 和 <xref:System.ServiceModel.ServiceAuthorizationManager> 的實作 (此實作會針對特定使用者將存取權限授予特定的服務方法)。 此樣本根據[訊息安全性使用者名稱](../../../../docs/framework/wcf/samples/message-security-user-name.md)，但會示範如何執行宣告轉換之前<xref:System.ServiceModel.ServiceAuthorizationManager>所呼叫。

> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。

 這個範例所示範的作業摘要如下：

- 用戶端可以使用使用者名稱與密碼來進行驗證。

- 用戶端可以使用 X.509 憑證進行驗證。

- 伺服器會向自訂 `UsernamePassword` 驗證器驗證用戶端認證。

- 伺服器是使用該伺服器的 X.509 憑證來驗證的。

- 伺服器可以使用 <xref:System.ServiceModel.ServiceAuthorizationManager> 來控制服務中特定方法的存取。

- 如何實作 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>。

服務會公開兩個端點，以便與使用組態檔 App.config 定義的服務進行通訊。每個端點是由位址、繫結及合約所組成。 其中一個繫結使用標準 `wsHttpBinding` 繫結 (使用 WS-Security 和用戶端使用者名稱驗證) 來設定。 另一個繫結使用標準 `wsHttpBinding` 繫結 (使用 WS-Security 和用戶端憑證驗證) 來設定。 [\<行為 >](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)指定要用於服務驗證的使用者認證。 伺服器憑證必須包含相同的值，如`SubjectName`屬性設為`findValue`屬性中[ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)。

```xml
<system.serviceModel>
  <services>
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <host>
        <baseAddresses>
          <!-- configure base address provided by host -->
          <add baseAddress ="http://localhost:8001/servicemodelsamples/service"/>
        </baseAddresses>
      </host>
      <!-- use base address provided by host, provide two endpoints -->
      <endpoint address="username"
                binding="wsHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
      <endpoint address="certificate"
                binding="wsHttpBinding"
                bindingConfiguration="Binding2"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>

  <bindings>
    <wsHttpBinding>
      <!-- Username binding -->
      <binding name="Binding1">
        <security mode="Message">
    <message clientCredentialType="UserName" />
        </security>
      </binding>
      <!-- X509 certificate binding -->
      <binding name="Binding2">
        <security mode="Message">
          <message clientCredentialType="Certificate" />
        </security>
      </binding>
    </wsHttpBinding>
  </bindings>

  <behaviors>
    <serviceBehaviors>
      <behavior name="CalculatorServiceBehavior" >
        <serviceDebug includeExceptionDetailInFaults ="true" />
        <serviceCredentials>
          <!--
          The serviceCredentials behavior allows one to specify a custom validator for username/password combinations.
          -->
          <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.MyCustomUserNameValidator, service" />
          <!--
          The serviceCredentials behavior allows one to specify authentication constraints on client certificates.
          -->
          <clientCertificate>
            <!--
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate
            is in the user's Trusted People store, then it will be trusted without performing a
            validation of the certificate's issuer chain. This setting is used here for convenience so that the
            sample can be run without having to have certificates issued by a certification authority (CA).
            This setting is less secure than the default, ChainTrust. The security implications of this
            setting should be carefully considered before using PeerOrChainTrust in production code.
            -->
            <authentication certificateValidationMode="PeerOrChainTrust" />
          </clientCertificate>
          <!--
          The serviceCredentials behavior allows one to define a service certificate.
          A service certificate is used by a client to authenticate the service and provide message protection.
          This configuration references the "localhost" certificate installed during the setup instructions.
          -->
          <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />
        </serviceCredentials>
        <serviceAuthorization serviceAuthorizationManagerType="Microsoft.ServiceModel.Samples.MyServiceAuthorizationManager, service">
          <!--
          The serviceAuthorization behavior allows one to specify custom authorization policies.
          -->
          <authorizationPolicies>
            <add policyType="Microsoft.ServiceModel.Samples.CustomAuthorizationPolicy.MyAuthorizationPolicy, PolicyLibrary" />
          </authorizationPolicies>
        </serviceAuthorization>
      </behavior>
    </serviceBehaviors>
  </behaviors>

</system.serviceModel>
```

每個用戶端的端點組態是由組態名稱、服務端點的絕對位址、繫結和合約所組成。 用戶端繫結已設定適當的安全性模式，指定在此情況下在[\<安全性 >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)並`clientCredentialType`中所指定[\<訊息 >](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md).

```xml
<system.serviceModel>

    <client>
      <!-- Username based endpoint -->
      <endpoint name="Username"
            address="http://localhost:8001/servicemodelsamples/service/username"
    binding="wsHttpBinding"
    bindingConfiguration="Binding1"
                behaviorConfiguration="ClientCertificateBehavior"
                contract="Microsoft.ServiceModel.Samples.ICalculator" >
      </endpoint>
      <!-- X509 certificate based endpoint -->
      <endpoint name="Certificate"
                        address="http://localhost:8001/servicemodelsamples/service/certificate"
                binding="wsHttpBinding"
            bindingConfiguration="Binding2"
                behaviorConfiguration="ClientCertificateBehavior"
                contract="Microsoft.ServiceModel.Samples.ICalculator">
      </endpoint>
    </client>

    <bindings>
      <wsHttpBinding>
        <!-- Username binding -->
      <binding name="Binding1">
        <security mode="Message">
          <message clientCredentialType="UserName" />
        </security>
      </binding>
        <!-- X509 certificate binding -->
        <binding name="Binding2">
          <security mode="Message">
            <message clientCredentialType="Certificate" />
          </security>
        </binding>
    </wsHttpBinding>
    </bindings>

    <behaviors>
      <behavior name="ClientCertificateBehavior">
        <clientCredentials>
          <serviceCertificate>
            <!--
            Setting the certificateValidationMode to PeerOrChainTrust
            means that if the certificate
            is in the user's Trusted People store, then it will be
            trusted without performing a
            validation of the certificate's issuer chain. This setting
            is used here for convenience so that the
            sample can be run without having to have certificates
            issued by a certification authority (CA).
            This setting is less secure than the default, ChainTrust.
            The security implications of this
            setting should be carefully considered before using
            PeerOrChainTrust in production code.
            -->
            <authentication certificateValidationMode = "PeerOrChainTrust" />
          </serviceCertificate>
        </clientCredentials>
      </behavior>
    </behaviors>

  </system.serviceModel>
```

針對使用者名稱架構的端點，用戶端實作會設定要使用的使用者名稱和密碼。

```csharp
// Create a client with Username endpoint configuration
CalculatorClient client1 = new CalculatorClient("Username");

client1.ClientCredentials.UserName.UserName = "test1";
client1.ClientCredentials.UserName.Password = "1tset";

try
{
    // Call the Add service operation.
    double value1 = 100.00D;
    double value2 = 15.99D;
    double result = client1.Add(value1, value2);
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);
    ...
}
catch (Exception e)
{
    Console.WriteLine("Call failed : {0}", e.Message);
}

client1.Close();
```

針對憑證架構的端點，用戶端實作會設定要使用的用戶端憑證。

```csharp
// Create a client with Certificate endpoint configuration
CalculatorClient client2 = new CalculatorClient("Certificate");

client2.ClientCredentials.ClientCertificate.SetCertificate(StoreLocation.CurrentUser, StoreName.My, X509FindType.FindBySubjectName, "test1");

try
{
    // Call the Add service operation.
    double value1 = 100.00D;
    double value2 = 15.99D;
    double result = client2.Add(value1, value2);
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);
    ...
}
catch (Exception e)
{
    Console.WriteLine("Call failed : {0}", e.Message);
}

client2.Close();
```

此範例使用自訂 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> 來驗證使用者名稱和密碼。 此範例會實作衍生自 `MyCustomUserNamePasswordValidator` 的 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>。 如需詳細資訊，請參閱 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> 相關文件。 為了示範與 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> 的整合，此自訂驗證器範例會實作 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 方法以接受使用者名稱/密碼組，以使其中的使用者名稱符合下列程式碼中所示的密碼。

```csharp
public class MyCustomUserNamePasswordValidator : UserNamePasswordValidator
{
  // This method validates users. It allows in two users,
  // test1 and test2 with passwords 1tset and 2tset respectively.
  // This code is for illustration purposes only and
  // MUST NOT be used in a production environment because it
  // is NOT secure.
  public override void Validate(string userName, string password)
  {
    if (null == userName || null == password)
    {
      throw new ArgumentNullException();
    }

    if (!(userName == "test1" && password == "1tset") && !(userName == "test2" && password == "2tset"))
    {
      throw new SecurityTokenException("Unknown Username or Password");
    }
  }
}
```

一旦驗證程式在服務程式碼中實作，服務主機就必須收到要使用的驗證程式執行個體的相關通知。 這是使用下列程式碼：

```csharp
Servicehost.Credentials.UserNameAuthentication.UserNamePasswordValidationMode = UserNamePasswordValidationMode.Custom;
serviceHost.Credentials.UserNameAuthentication.CustomUserNamePasswordValidator = new MyCustomUserNamePasswordValidatorProvider();
```

或者，您可以在組態中相同的動作：

```xml
<behavior ...>
    <serviceCredentials>
      <!--
      The serviceCredentials behavior allows one to specify a custom validator for username/password combinations.
      -->
      <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.MyCustomUserNameValidator, service" />
    ...
    </serviceCredentials>
</behavior>
```

Windows Communication Foundation (WCF) 提供豐富的宣告式模型來執行存取檢查。 <xref:System.ServiceModel.ServiceAuthorizationManager> 物件會被用來執行存取檢查並判斷與用戶端相關的宣告是否能夠滿足存取服務方法所需的必要需求。

針對示範目的，此範例會示範如何實作<xref:System.ServiceModel.ServiceAuthorizationManager>可實<xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A>宣告的型別為基礎的方法，以允許使用者的存取方法`http://example.com/claims/allowedoperation`其值會是此作業之動作 URI允許呼叫。

```csharp
public class MyServiceAuthorizationManager : ServiceAuthorizationManager
{
  protected override bool CheckAccessCore(OperationContext operationContext)
  {
    string action = operationContext.RequestContext.RequestMessage.Headers.Action;
    Console.WriteLine("action: {0}", action);
    foreach(ClaimSet cs in operationContext.ServiceSecurityContext.AuthorizationContext.ClaimSets)
    {
      if ( cs.Issuer == ClaimSet.System )
      {
        foreach (Claim c in cs.FindClaims("http://example.com/claims/allowedoperation", Rights.PossessProperty))
        {
          Console.WriteLine("resource: {0}", c.Resource.ToString());
          if (action == c.Resource.ToString())
            return true;
        }
      }
    }
    return false;
  }
}
```

一旦實作了自訂 <xref:System.ServiceModel.ServiceAuthorizationManager>，就必須告知服務主機要使用的 <xref:System.ServiceModel.ServiceAuthorizationManager>。 執行方式如下列程式碼所示。

```xml
<behavior ...>
    ...
    <serviceAuthorization serviceAuthorizationManagerType="Microsoft.ServiceModel.Samples.MyServiceAuthorizationManager, service">
        ...
    </serviceAuthorization>
</behavior>
```

要實作的主要 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 方法為 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法。

```csharp
public class MyAuthorizationPolicy : IAuthorizationPolicy
{
    string id;

    public MyAuthorizationPolicy()
    {
    id =  Guid.NewGuid().ToString();
    }

    public bool Evaluate(EvaluationContext evaluationContext,
                                            ref object state)
    {
        bool bRet = false;
        CustomAuthState customstate = null;

        if (state == null)
        {
            customstate = new CustomAuthState();
            state = customstate;
        }
        else
            customstate = (CustomAuthState)state;
        Console.WriteLine("In Evaluate");
        if (!customstate.ClaimsAdded)
        {
           IList<Claim> claims = new List<Claim>();

           foreach (ClaimSet cs in evaluationContext.ClaimSets)
              foreach (Claim c in cs.FindClaims(ClaimTypes.Name,
                                         Rights.PossessProperty))
                  foreach (string s in
                        GetAllowedOpList(c.Resource.ToString()))
                  {
                       claims.Add(new
               Claim("http://example.com/claims/allowedoperation",
                                    s, Rights.PossessProperty));
                            Console.WriteLine("Claim added {0}", s);
                      }
                   evaluationContext.AddClaimSet(this,
                           new DefaultClaimSet(this.Issuer,claims));
                   customstate.ClaimsAdded = true;
                   bRet = true;
                }
         else
         {
              bRet = true;
         }
         return bRet;
     }
...
}
```

前一段程式碼說明 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法會檢查並確定未新增任何會影響處理的新宣告，然後再新增特定宣告。 允許的宣告是從 `GetAllowedOpList` 方法取得，此方法經過實作，會傳回可供使用者執行的特定作業清單。 授權原則會新增宣告以便處理特定作業。 此宣告稍後會由 <xref:System.ServiceModel.ServiceAuthorizationManager> 使用，以執行存取檢查決策。

一旦實作了自訂 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>，就必須告知服務主機要使用的授權原則。

```xml
<serviceAuthorization ...>
       <authorizationPolicies>
            <add policyType='Microsoft.ServiceModel.Samples.CustomAuthorizationPolicy.MyAuthorizationPolicy, PolicyLibrary' />
       </authorizationPolicies>
</serviceAuthorization>
```

當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 用戶端會順利呼叫 Add、Subtract 和 Multiple 方法，並在嘗試呼叫 Divide 方法時取得「拒絕存取」訊息。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。

## <a name="setup-batch-file"></a>設定批次檔

本範例中所包含的 Setup.bat 批次檔可讓您使用相關的憑證設定伺服器，以執行需要伺服器憑證安全性的自我裝載應用程式。

下面提供批次檔的各區段簡要概觀，讓批次檔得以修改為在適當的組態下執行：

- 建立伺服器憑證。

    下列 Setup.bat 批次檔中的程式行會建立要使用的伺服器憑證。 %SERVER_NAME% 變數會指定伺服器名稱。 您可以變更這個變數來指定自己的伺服器名稱。 預設值為 localhost。

    ```
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- 將伺服器憑證安裝至用戶端的受信任憑證存放區中。

    Setup.bat 批次檔中的下列程式行會將伺服器憑證複製到用戶端受信任人的存放區。 這是必要步驟，因為用戶端系統並未隱含信任 Makecert.exe 產生的憑證。 如果您已經有一個以用戶端信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將伺服器憑證填入用戶端憑證存放區的步驟。

    ```
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- 建立用戶端憑證。

    下列 Setup.bat 批次檔中的程式行會建立要使用的用戶端憑證。 %USER_NAME% 變數會指定伺服器名稱。 這個值會設定為 "test1"，因為這是 `IAuthorizationPolicy` 會尋找的名稱。 如果變更了 %USER_NAME% 的值，您就必須在 `IAuthorizationPolicy.Evaluate` 方法中變更對應的值。

    憑證會儲存在 CurrentUser 存放區位置下的 My (Personal) 存放區中。

    ```
    echo ************
    echo making client cert
    echo ************
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe
    ```

- 將用戶端憑證安裝至伺服器的受信任憑證存放區中。

    Setup.bat 批次檔中的下列程式行會將用戶端憑證複製到受信任人的存放區。 這是必要步驟，因為伺服器系統並未隱含信任 Makecert.exe 產生的憑證。 如果您已經有一個以信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將用戶端憑證填入伺服器憑證存放區的步驟。

    ```
    certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople
    ```

### <a name="to-set-up-and-build-the-sample"></a>若要設定和建置範例

1. 若要建置方案時，請依照中的指示[建置 Windows Communication Foundation 範例](../../../../docs/framework/wcf/samples/building-the-samples.md)。

2. 若要在單一或跨電腦的組態中執行本範例，請使用下列指示。

> [!NOTE]
> 如果您使用 Svcutil.exe 重新產生這個範例的組態，請務必修改用戶端組態中的端點名稱，以符合用戶端程式碼。

### <a name="to-run-the-sample-on-the-same-computer"></a>若要在同一部電腦上執行範例

1. 開啟系統管理員權限適用於 Visual Studio 開發人員命令提示字元並執行*Setup.bat*從範例安裝資料夾。 這會安裝執行範例所需的所有憑證。

    > [!NOTE]
    > Setup.bat 批次檔被設計來執行適用於 Visual Studio 從開發人員命令提示字元。 Visual Studio 指向包含所需的可執行檔的目錄路徑環境變數設定在 「 開發人員命令提示字元*Setup.bat*指令碼。

1. 從啟動 Service.exe *service\bin*。

1. 從啟動 Client.exe *\client\bin* 。 用戶端活動會顯示在用戶端主控台應用程式上。

如果用戶端和服務能夠進行通訊，請參閱[的 WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。

### <a name="to-run-the-sample-across-computers"></a>若要跨電腦執行範例

1. 在服務電腦上建立目錄。

2. 從服務程式檔複製 *\service\bin*到服務電腦上的目錄。 同時將 Setup.bat、Cleanup.bat、GetComputerName.vbs 和 ImportClientCert.bat 檔複製到服務電腦上。

3. 在用戶端電腦上為用戶端二進位碼檔案建立一個目錄。

4. 將用戶端程式檔複製到用戶端電腦上的用戶端目錄。 同時，將 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 檔案複製到用戶端。

5. 在伺服器上，執行`setup.bat service`中開發人員命令提示字元使用系統管理員權限開啟的 Visual Studio。

    執行`setup.bat`具有`service`引數建立電腦的完整的網域名稱服務憑證，並將服務憑證匯出至名為的檔案*Service.cer*。

6. 編輯*Service.exe.config*以反映新的憑證名稱 (在`findValue`屬性中[ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)) 這是完整的網域名稱相同電腦。 也會變更**computername**中\<服務 > /\<baseAddresses > 項目服務電腦的完整名稱從 localhost。

7. 複製*Service.cer*檔案從服務目錄至用戶端目錄用戶端電腦上的。

8. 在用戶端，執行`setup.bat client`中開發人員命令提示字元使用系統管理員權限開啟的 Visual Studio。

    執行`setup.bat`具有`client`引數會建立名為用戶端憑證**test1** ，並將用戶端憑證匯出為名為檔案*Client.cer*。

9. 在  *Client.exe.config*檔案在用戶端電腦上，變更端點位址值以符合您的服務的新位址。 執行這項操作來取代**localhost**伺服器的完整的網域名稱。

10. 從用戶端目錄將 Client.cer 檔案複製到伺服器上的服務目錄中。

11. 在用戶端，執行*ImportServiceCert.bat*中開發人員命令提示字元使用系統管理員權限開啟的 Visual Studio。

    這會在將服務憑證從 Service.cer 檔案匯入**CurrentUser-TrustedPeople**儲存。

12. 在伺服器上，執行*ImportClientCert.bat*中開發人員命令提示字元使用系統管理員權限開啟的 Visual Studio。

    這會從 Client.cer 檔案匯入的用戶端憑證**LocalMachine-TrustedPeople**儲存。

13. 在伺服器電腦上，從命令提示字元視窗啟動 Service.exe。

14. 在用戶端電腦上，從命令提示字元視窗啟動 Client.exe。

    如果用戶端和服務能夠進行通訊，請參閱[的 WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。

### <a name="clean-up-after-the-sample"></a>在此範例之後進行清除

若要清除在此範例之後，執行*Cleanup.bat*當您完成執行範例中的 [samples] 資料夾中。 這樣會從憑證存放區中移除伺服器與用戶端憑證。

> [!NOTE]
> 跨電腦執行此範例時，這個指令碼不會移除用戶端上的服務憑證。 如果您已執行 WCF 範例，在電腦之間使用的憑證，請務必清除的服務憑證已安裝在 CurrentUser-TrustedPeople 存放。 若要這樣做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` 例如： `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。

---
title: Comportamentos de segurança no WCF
ms.date: 03/30/2017
ms.assetid: 513232c0-39fd-4409-bda6-5ebd5e0ea7b0
author: BrucePerlerMS
manager: mbaldwin
ms.openlocfilehash: 57bd34c72e98091c4a429d683a0da4ce2d3967c0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33508638"
---
# <a name="security-behaviors-in-wcf"></a>Comportamentos de segurança no WCF
No Windows Communication Foundation (WCF), comportamentos de modificar o comportamento de tempo de execução no nível de serviço ou no nível do ponto de extremidade. (Para obter mais informações sobre comportamentos em geral, consulte [especificando comportamento de tempo de execução do serviço](../../../../docs/framework/wcf/specifying-service-run-time-behavior.md).) *Comportamentos de segurança* permitem o controle sobre as credenciais, autenticação, autorização e logs de auditoria. Você pode usar comportamentos por programação ou por meio da configuração. Este tópico se concentra na configuração os seguintes comportamentos relacionados às funções de segurança:  
  
-   [\<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md).  
  
-   [\<clientCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md).  
  
-   [\<serviceAuthorization >](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md).  
  
-   [\<serviceSecurityAudit >](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md).  
  
-   [\<serviceMetadata >](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md), que também permite que você especifique um ponto de extremidade seguro que os clientes podem acessar para metadados.  
  
## <a name="setting-credentials-with-behaviors"></a>Configuração de credenciais com comportamentos  
 Use o [ \<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) e [ \<clientCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) para definir valores de credencial para um serviço ou cliente. A configuração de associação subjacente determina se uma credencial deve ser definida. Por exemplo, se o modo de segurança é definido como `None`, clientes e serviços não autentiquem uns aos outros e não requerer nenhuma credencial de qualquer tipo.  
  
 Por outro lado, a associação de serviço pode exigir um tipo de credencial de cliente. Nesse caso, você precisará definir um valor de credencial usando um comportamento. (Para obter mais informações sobre os possíveis tipos de credenciais, consulte [selecionando um tipo de credencial](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md).) Em alguns casos, como quando as credenciais do Windows são usadas para autenticar, o ambiente estabelece automaticamente o valor de credencial real e você não precisa definir explicitamente o valor de credencial (a menos que você deseja especificar um conjunto diferente de credenciais).  
  
 Todas as credenciais de serviço são encontradas como elementos filho de [ \<serviceBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md). O exemplo a seguir mostra um certificado usado como uma credencial de serviço.  
  
```xml  
<configuration>  
 <system.serviceModel>  
  <behaviors>  
   <serviceBehaviors>  
    <behavior name="ServiceBehavior1">  
     <serviceCredentials>  
      <serviceCertificate findValue="000000000000000000000000000"   
                          storeLocation="CurrentUser"  
      storeName="Root" x509FindType="FindByThumbprint" />  
     </serviceCredentials>  
    </behavior>  
   </serviceBehaviors>  
  </behaviors>  
 </system.serviceModel>  
</configuration>  
```  
  
## <a name="service-credentials"></a>Credenciais de serviço  
 O [ \<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) contém quatro elementos filho. Os elementos e seus usos são discutidos nas seções a seguir.  
  
### <a name="servicecertificate-element"></a>\<serviceCertificate > elemento  
 Use esse elemento para especificar um certificado x. 509 que é usado para autenticar o serviço para clientes usando o modo de segurança de mensagem. Se você estiver usando um certificado que é periodicamente renovada, em seguida, suas alterações de impressão digital. Nesse caso, use o nome da entidade como o `X509FindType` porque o certificado pode ser reemitido com o mesmo nome de assunto.  
  
 Para obter mais informações sobre como usar o elemento, consulte [como: especificar valores de credencial de cliente](../../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
### <a name="certificate-of-clientcertificate-element"></a>\<certificado > de \<clientCertificate > elemento  
 Use o [ \<certificado >](../../../../docs/framework/configure-apps/file-schema/wcf/certificate-of-clientcertificate-element.md) elemento quando o serviço deve ter o certificado do cliente com antecedência para comunicação segura com o cliente. Isso ocorre ao usar o padrão de comunicação duplex. O padrão mais comum de solicitação-resposta, o cliente inclui o seu certificado na solicitação, o serviço usa para proteger sua resposta ao cliente. O padrão de comunicação duplex, no entanto, não tem solicitações e respostas. O serviço não é possível inferir o certificado do cliente da comunicação e, portanto, o serviço requer que o certificado do cliente com antecedência para proteger as mensagens para o cliente. Você deve obter o certificado do cliente de uma maneira de fora de banda e especificar o certificado usando esse elemento. Para obter mais informações sobre serviços de duplex, consulte [como: criar um contrato Duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md).  
  
### <a name="authentication-of-clientcertificate-element"></a>\<autenticação > de \<clientCertificate > elemento  
 O [ \<autenticação >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md) elemento permite que você personalize a forma como os clientes são autenticados. Você pode definir o `CertificateValidationMode` atributo `None`, `ChainTrust`, `PeerOrChainTrust`, `PeerTrust`, ou `Custom`. Por padrão, o nível é definido como `ChainTrust`, que especifica que cada certificado deve ser encontrado em uma hierarquia de certificados terminam em um *autoridade raiz* na parte superior da cadeia. Este é o modo mais seguro. Você também pode definir o valor `PeerOrChainTrust`, que especifica que os certificados emitidos por conta própria (confiança ponto a ponto) são aceitos, bem como certificados que estão em uma cadeia confiável. Esse valor é usado durante o desenvolvimento e depuração clientes e serviços, pois os certificados emitidos por conta própria não precisam ser adquiridos de uma autoridade confiável. Ao implantar um cliente, use o `ChainTrust` valor em vez disso. Você também pode definir o valor `Custom`. Quando definido como o `Custom` valor, você também deve definir o `CustomCertificateValidatorType` de atributo para um assembly e o tipo usado para validar o certificado. Para criar seu próprios validador personalizado, você deve herdar de abstrata <xref:System.IdentityModel.Selectors.X509CertificateValidator> classe.  
  
### <a name="issuedtokenauthentication-element"></a>\<issuedTokenAuthentication > elemento  
 O cenário de token emitido tem três etapas. O primeiro estágio, um cliente tentar acessar um serviço é chamado um *do serviço de token seguro* (STS). O STS subsequentemente problemas o cliente um token, normalmente um token de segurança asserções SAML (Markup Language) e, em seguida, autentica o cliente. O cliente, em seguida, retorne para o serviço com o token. O serviço examina o token de dados que permite que o serviço autenticar o token e, portanto, o cliente. Para autenticar o token, o certificado que usa o serviço de token de seguro deve ser conhecido para o serviço. O [ \<issuedTokenAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md) elemento é o repositório de todos esses certificados de serviço de token seguro. Para adicionar certificados, use o [ \<knownCertificates >](../../../../docs/framework/configure-apps/file-schema/wcf/knowncertificates.md). Inserir uma [ \<Adicionar >](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-knowncertificates.md) para cada certificado, conforme mostrado no exemplo a seguir.  
  
```xml  
<issuedTokenAuthentication>  
   <knownCertificates>  
      <add findValue="www.contoso.com"   
           storeLocation="LocalMachine" storeName="My"   
           X509FindType="FindBySubjectName" />  
    </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
 Por padrão, os certificados devem ser obtidos de um serviço de token seguro. Esses "conhecidos" certificados Certifique-se de que apenas legítimas clientes podem acessar um serviço.  
  
 Você deve usar o [ \<allowedAudienceUris >](../../../../docs/framework/configure-apps/file-schema/wcf/allowedaudienceuris.md) coleção em um aplicativo federado que utiliza um *do serviço de token seguro* (STS) que emite `SamlSecurityToken` tokens de segurança. Quando o STS emite o token de segurança, ele pode especificar o URI dos serviços da Web para o qual o token de segurança destina-se com a adição de um `SamlAudienceRestrictionCondition` para o token de segurança. Que permite que o `SamlSecurityTokenAuthenticator` para o serviço Web destinatário verificar se o token de segurança emitido destina-se para esse serviço da Web, especificando que essa seleção deve acontecer, fazendo o seguinte:  
  
-   Definir o `audienceUriMode` atributo de [ \<issuedTokenAuthentication >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md) para `Always` ou `BearerKeyOnly`.  
  
-   Especifique o conjunto de URIs válidos, adicionando os URIs a esta coleção. Para fazer isso, insira uma [ \<Adicionar >](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-allowedaudienceuris.md) para cada URI  
  
 Para obter mais informações, consulte <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.  
  
 Para obter mais informações sobre este elemento de configuração, consulte [como: configurar credenciais em um serviço de Federação](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).  
  
#### <a name="allowing-anonymous-cardspace-users"></a>Permitir que usuários anônimos CardSpace  
 Definindo o `AllowUntrustedRsaIssuers` atributo do `<IssuedTokenAuthentication>` elemento `true` explicitamente permite que qualquer cliente apresentar um token emitido por conta própria assinado com um par de chaves RSA arbitrário. O emissor é *não confiável* porque a chave não tem nenhum dado de emissor associado a ele. Um [!INCLUDE[infocard](../../../../includes/infocard-md.md)] usuário pode criar um cartão emitido por conta própria que inclui automaticamente fornecidas declarações de identidade. Use esse recurso com cuidado. Para usar esse recurso, considere a chave pública RSA como uma senha mais segura que deve ser armazenada em um banco de dados juntamente com um nome de usuário. Antes de permitir o acesso de cliente ao serviço, verifique se a chave pública RSA apresentada pelo cliente, comparando-o com a chave pública armazenada para o nome de usuário apresentada. Isso pressupõe que você estabelecer um processo de registro no qual os usuários podem registrar seus nomes de usuário e associá-los com as chaves públicas do RSA emitidas por conta própria.  
  
## <a name="client-credentials"></a>Credenciais do cliente  
 As credenciais do cliente são usadas para autenticar o cliente para serviços em casos em que a autenticação mútua é necessária. Você pode usar a seção para especificar os certificados de serviço para cenários em que o cliente deve proteger as mensagens para um serviço com o certificado do serviço.  
  
 Você também pode configurar um cliente como parte de um cenário de federação para tokens emitido de uso de um serviço de token seguro ou um emissor local de tokens. Para obter mais informações sobre cenários federados, consulte [federação e Tokens emitidos](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md). Todas as credenciais de cliente estão localizadas sob o [ \<endpointBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md), conforme mostrado no código a seguir.  
  
```xml  
<behaviors>  
 <endpointBehaviors>  
  <behavior name="EndpointBehavior1">  
   <clientCredentials>  
    <clientCertificate findValue="cn=www.contoso.com"     
        storeLocation="LocalMachine"  
        storeName="AuthRoot" x509FindType="FindBySubjectName" />  
    <serviceCertificate>  
     <defaultCertificate findValue="www.cohowinery.com"   
                    storeLocation="LocalMachine"  
                    storeName="Root" x509FindType="FindByIssuerName" />  
    <authentication revocationMode="Online"  
                    trustedStoreLocation="LocalMachine" />  
    </serviceCertificate>  
   </clientCredentials>  
  </behavior>  
 </endpointBehaviors>  
```  
  
#### <a name="clientcertifictate-element"></a>\<clientCertifictate > elemento  
 Defina o certificado usado para autenticar o cliente com esse elemento. Para obter mais informações, consulte [como: especificar valores de credencial de cliente](../../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
#### <a name="httpdigest"></a>\<httpDigest >  
 Esse recurso deve ser habilitado com o Active Directory no Windows e serviços de informações da Internet (IIS). Para obter mais informações, consulte [a autenticação Digest no IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=88443).  
  
#### <a name="issuedtoken-element"></a>\<issuedToken > elemento  
 O [ \<issuedToken >](../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md) contém os elementos usados para configurar um emissor local de tokens ou comportamentos usados com um serviço de token de segurança. Para obter instruções sobre como configurar um cliente para usar um emissor local, consulte [como: configurar um emissor Local](../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md).  
  
#### <a name="localissueraddress"></a>\<localIssuerAddress >  
 Especifica um endereço de serviço de token de segurança padrão. Isso é usado quando o <xref:System.ServiceModel.WSFederationHttpBinding> não fornecer uma URL para o serviço de token de segurança, ou quando o endereço do emissor de uma associação federada é http://schemas.microsoft.com/2005/12/ServiceModel/Addressing/Anonymous ou `null`. Nesses casos, o <xref:System.ServiceModel.Description.ClientCredentials> deve ser configurado com o endereço do emissor local e a associação a ser usado para se comunicar com esse emissor.  
  
#### <a name="issuerchannelbehaviors"></a>\<issuerChannelBehaviors >  
 Use o [ \<issuerChannelBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/issuerchannelbehaviors-element.md) para adicionar os comportamentos do cliente WCF usados ao se comunicar com um serviço de token de segurança. Definem os comportamentos do cliente no [ \<endpointBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md) seção. Para usar um comportamento definido, adicione um <`add`> elemento para o `<issuerChannelBehaviors>` elemento com dois atributos. Definir o `issuerAddress` para a URL do serviço de token de segurança e definir o `behaviorConfiguration` de atributo para o nome do comportamento do ponto de extremidade definido, conforme mostrado no exemplo a seguir.  
  
```xml  
<clientCredentials>  
   <issuedToken>  
      <issuerChannelBehaviors>  
         <add issuerAddress="http://www.contoso.com"  
               behaviorConfiguration="clientBehavior1" />     
```  
  
#### <a name="servicecertificate-element"></a>\<serviceCertificate > elemento  
 Use esse elemento para controlar a autenticação de certificados de serviço.  
  
 O [ \<defaultCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/defaultcertificate-element.md) elemento pode armazenar um único certificado usado quando o serviço não especifica nenhum certificado.  
  
 Use o [ \<scopedCertificates >](../../../../docs/framework/configure-apps/file-schema/wcf/scopedcertificates-element.md) e [ \<Adicionar >](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-scopedcertificates-element.md) configurar certificados de serviço que estão associados a serviços específicos. O `<add>` elemento inclui um `targetUri` atributo que é usado para associar o certificado com o serviço.  
  
 O [ \<autenticação >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) elemento Especifica o nível de confiança usado para autenticar certificados. Por padrão, o nível é definido como "ChainTrust", que especifica que cada certificado deve ser encontrado em uma hierarquia de certificados terminam em uma autoridade de certificação confiável na parte superior da cadeia. Este é o modo mais seguro. Você também pode definir o valor "PeerOrChainTrust", que especifica que os certificados emitidos por conta própria (confiança ponto a ponto) são aceitos, bem como certificados que estão em uma cadeia confiável. Esse valor é usado durante o desenvolvimento e depuração clientes e serviços, pois os certificados emitidos por conta própria não precisam ser adquiridos de uma autoridade confiável. Ao implantar um cliente, use o valor de "ChainTrust". Você também pode definir o valor para "Custom" ou "None". Para usar o valor de "Custom", você também deve definir o `CustomCertificateValidatorType` de atributo para um assembly e o tipo usado para validar o certificado. Para criar seu próprios validador personalizado, você deve herdar de abstrata <xref:System.IdentityModel.Selectors.X509CertificateValidator> classe. Para obter mais informações, consulte [como: criar um serviço que utiliza um validador de certificado personalizado](../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).  
  
 O [ \<autenticação >](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md) elemento inclui um `RevocationMode` atributo que especifica como os certificados são verificados para revogação. O padrão é "online", que indica que os certificados são automaticamente verificados para revogação. Para obter mais informações, consulte [trabalhar com certificados](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
## <a name="serviceauthorization"></a>ServiceAuthorization  
 O [ \<serviceAuthorization >](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md) elemento contém elementos que afetam a autorização, provedores de função personalizada e representação.  
  
 O <xref:System.Security.Permissions.PrincipalPermissionAttribute> classe é aplicada a um método de serviço. O atributo especifica os grupos de usuários para usar ao autorizar o uso de um método protegido. O valor padrão é "UseWindowsGroups" e especifica que os grupos do Windows, como "Administradores" ou "Usuários" são pesquisados para uma tentativa de acessar um recurso de identidade. Você também pode especificar "UseAspNetRoles" para usar um provedor de função personalizada que está configurado com o <`system.web` > elemento, conforme mostrado no código a seguir.  
  
```xml  
<system.web>  
  <membership defaultProvider="SqlProvider"   
   userIsOnlineTimeWindow="15">  
     <providers>  
       <clear />  
       <add   
          name="SqlProvider"   
          type="System.Web.Security.SqlMembershipProvider"   
          connectionStringName="SqlConn"  
          applicationName="MembershipProvider"  
          enablePasswordRetrieval="false"  
          enablePasswordReset="false"  
          requiresQuestionAndAnswer="false"  
          requiresUniqueEmail="true"  
          passwordFormat="Hashed" />  
     </providers>  
   </membership>  
  <!-- Other configuration code not shown.-->  
</system.web>  
```  
  
 O código a seguir mostra o `roleProviderName` usado com o `principalPermissionMode` atributo.  
  
```xml  
<behaviors>  
 <behavior name="ServiceBehaviour">          
  <serviceAuthorization principalPermissionMode ="UseAspNetRoles"   
                        roleProviderName ="SqlProvider" />  
</behavior>   
   <!-- Other configuration code not shown. -->  
</behaviors>  
```  
  
## <a name="configuring-security-audits"></a>Configurar auditorias de segurança  
 Use o [ \<serviceSecurityAudit >](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md) para especificar o log gravado e quais tipos de eventos de log. Para obter mais informações, consulte [auditoria](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  
  
```xml  
<system.serviceModel>  
<serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceSecurityAudit auditLogLocation="Application"   
             suppressAuditFailure="true"  
             serviceAuthorizationAuditLevel="Success"   
             messageAuthenticationAuditLevel="Success" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
## <a name="secure-metadata-exchange"></a>Proteger a troca de metadados  
 Exportação de metadados para clientes é conveniente para desenvolvedores de cliente e de serviço, pois permite downloads de código do cliente e configuração. Para reduzir a exposição de um serviço a usuários mal-intencionados, é possível proteger a transferência usando o SSL em mecanismo de HTTP (HTTPS). Para fazer isso, primeiro você deve ligar um certificado x. 509 apropriado para uma porta específica no computador que hospeda o serviço. (Para obter mais informações, consulte [trabalhar com certificados](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).) Em seguida, adicione um [ \<serviceMetadata >](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md) para a configuração do serviço e defina o `HttpsGetEnabled` atributo `true`. Finalmente, defina o `HttpsGetUrl` atributo para a URL do ponto de extremidade de metadados de serviço, conforme mostrado no exemplo a seguir.  
  
```xml  
<behaviors>  
 <serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceMetadata httpsGetEnabled="true"   
     httpsGetUrl="https://myComputerName/myEndpoint" />  
  </behavior>  
 </serviceBehaviors>  
</behaviors>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Auditoria](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)  
 [Modelo de segurança para o Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)

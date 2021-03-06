---
title: '방법: 보안 세션 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], creating a session
ms.assetid: b6f42b5a-bbf7-45cf-b917-7ec9fa7ae110
ms.openlocfilehash: 80973a31050cf1ede03d4a3919066c62625ae590
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593414"
---
# <a name="how-to-create-a-secure-session"></a>방법: 보안 세션 만들기
바인딩을 제외 하 고 [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) , WCF (Windows Communication Foundation)의 시스템 제공 바인딩은 메시지 보안을 사용 하는 경우 자동으로 보안 세션을 사용 합니다.  
  
 기본적으로 보안 세션은 재생된 웹 서버에 남지 않습니다. 보안 세션이 설정되면 클라이언트와 서비스에서 보안 세션과 연결된 키를 캐시합니다. 메시지를 교환하면 캐시된 키의 식별자만 교환됩니다. 웹 서버가 재생되면 캐시도 재생되며, 이 때 웹 서버는 식별자의 캐시된 키를 검색할 수 없습니다. 이런 경우가 발생하면 클라이언트로 예외가 throw됩니다. 상태 저장 SCT(보안 컨텍스트 토큰)을 사용하는 보안 세션은 웹 서버가 재생되는 동안 보안 세션을 유지할 수 있습니다. 보안 세션에서 상태 저장 SCT를 사용 하는 방법에 대 한 자세한 내용은 [방법: 보안 세션에 대 한 보안 컨텍스트 토큰 만들기](how-to-create-a-security-context-token-for-a-secure-session.md)를 참조 하세요.  
  
### <a name="to-specify-that-a-service-uses-secure-sessions-by-using-one-of-the-system-provided-bindings"></a>서비스에서 시스템에서 제공되는 바인딩 중 하나를 사용하여 보안 세션을 사용하도록 지정하려면  
  
- 메시지 보안을 지원하는 시스템 제공 바인딩을 사용하도록 서비스를 구성합니다.  
  
     바인딩을 제외 하 고 [\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md) 시스템 제공 바인딩이 메시지 보안을 사용 하도록 구성 된 경우 WCF는 자동으로 보안 세션을 사용 합니다. 다음 표에는 메시지 보안을 지원하는 시스템 제공 바인딩과 메시지 보안이 기본 보안 메커니즘인지 여부가 표시되어 있습니다.  
  
    |시스템 제공 바인딩|구성 요소|기본적으로 메시지 보안 사용|  
    |------------------------------|---------------------------|------------------------------------|  
    |<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding>](../../configure-apps/file-schema/wcf/basichttpbinding.md)|예|  
    |<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md)|예|  
    |<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding>](../../configure-apps/file-schema/wcf/wsdualhttpbinding.md)|예|  
    |<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding>](../../configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|예|  
    |<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md)|아니요|  
    |<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding>](../../configure-apps/file-schema/wcf/netmsmqbinding.md)|예|  
  
     다음 코드 예제에서는 구성을 사용 하 여 `wsHttpBinding_Calculator` [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) , 메시지 보안 및 보안 세션을 사용 하는 라는 바인딩을 지정 합니다.  
  
    ```xml  
    <bindings>  
      <WSHttpBinding>  
       <binding name = "wsHttpBinding_Calculator">  
         <security mode="Message">  
           <message clientCredentialType="Windows"/>  
         </security>  
        </binding>  
      </WSHttpBinding>  
    </bindings>  
    ```  
  
     다음 코드 예제에서는 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) , 메시지 보안 및 보안 세션을 사용 하 여 서비스를 보호 하도록 지정 합니다 `secureCalculator` .  
  
     [!code-csharp[c_CreateSecureSession#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#1)]
     [!code-vb[c_CreateSecureSession#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#1)]  
  
    > [!NOTE]
    > 에서 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) 특성을로 설정 하 여 보안 세션을 해제할 수 있습니다 `establishSecurityContext` `false` . 다른 시스템 제공 바인딩의 경우 사용자 지정 바인딩을 만들어야만 보안 세션을 끌 수 있습니다.  
  
### <a name="to-specify-that-a-service-uses-secure-sessions-by-using-a-custom-binding"></a>사용자 지정 바인딩을 사용하여 서비스에서 보안 세션을 사용하도록 지정하려면  
  
- 보안 세션을 통해 SOAP 메시지를 보호하도록 지정하는 사용자 지정 바인딩을 만듭니다.  
  
     사용자 지정 바인딩을 만드는 방법에 대 한 자세한 내용은 [방법: 시스템 제공 바인딩 사용자 지정](../extending/how-to-customize-a-system-provided-binding.md)을 참조 하세요.  
  
     다음 코드 예제에서는 구성을 사용하여 보안 세션을 통해 메시지를 전송하는 사용자 지정 바인딩을 지정합니다.  
  
    ```xml  
    <bindings>  
      <!-- configure a custom binding -->  
      <customBinding>  
        <binding name="customBinding_Calculator">  
          <security authenticationMode="SecureConversation" />  
          <secureConversationBootstrap authenticationMode="SspiNegotiated" />  
          <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8"/>  
          <httpTransport/>  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
     다음 코드 예제에서는 <xref:System.ServiceModel.Configuration.AuthenticationMode.MutualCertificate> 인증 모드를 사용하여 보안 세션을 부트스트랩하는 사용자 지정 바인딩을 만듭니다.  
  
     [!code-csharp[c_CreateSecureSession#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#2)]
     [!code-vb[c_CreateSecureSession#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#2)]  
  
## <a name="see-also"></a>참고 항목

- [WCF 바인딩 개요](../bindings-overview.md)

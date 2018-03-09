---
title: "연결 및 세션 (XMLA) 관리 | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- statefulness [XML for Analysis]
- statelessness [XML for Analysis]
- XML for Analysis, sessions
- states [XML for Analysis]
- XMLA, sessions
- sessions [XML for Analysis]
ms.assetid: b83bb3ff-09be-4fda-9d1d-6248e04ffb21
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 761618d7a0d651fb24257e03c5fcb261fde051c6
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="managing-connections-and-sessions-xmla"></a>연결 및 세션 관리(XMLA)
  *상태 저장* id와 컨텍스트 메서드 호출 간에 클라이언트의 서버에서 유지 하는 조건입니다. *상태 비저장* 는 서버 기억 하지 id와 클라이언트의 컨텍스트 메서드 호출이 완료 된 후 상태입니다.  
  
 XML for Analysis (XMLA)은 상태 저장을 제공 하려면 다음을 지원 합니다. *세션* 일련의 문 함께 수행할 수 있도록 합니다. 예를 들어, 이러한 일련의 문을 사용하여 후속 쿼리에서 사용할 계산 멤버를 만들 수 있습니다.  
  
 일반적으로 XMLA의 세션은 OLE DB 2.6 사양에 설명된 다음과 같은 동작을 따릅니다.  
  
-   세션에는 트랜잭션 및 명령 컨텍스트 범위가 정의됩니다.  
  
-   단일 세션 컨텍스트에서 여러 명령을 실행할 수 있습니다.  
  
-   XMLA 컨텍스트의 트랜잭션은 지원은 함께 전송 되는 공급자별 명령을 통해는 [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
 XMLA에는 느슨하게 연결된 환경에서 잠금을 구현하기 위해 DAV(Distributed Authoring and Versioning) 프로토콜에서 사용하는 방법과 비슷한 모드로 웹 환경에서 세션을 지원하는 방법이 정의되어 있습니다. 이 구현은 공급자가 제한 시간, 연결 오류 등의 여러 가지 이유로 세션을 만료시킬 수 있다는 점에서 DAV와 같습니다. 세션이 지원되는 경우 웹 서비스는 다시 시작해야 하는 중단된 명령 집합을 인식하고 처리할 수 있어야 합니다.  
  
 W3C(World Wide Web Consortium) SOAP(Simple Object Access Protocol) 사양에서는 SOAP 헤더를 사용하여 SOAP 메시지 위에 새 프로토콜을 작성할 것을 권장합니다. 다음 표에서는 세션 시작, 유지 관리 및 닫기를 위해 XMLA에 정의된 SOAP 헤더 요소 및 특성을 설명합니다.  
  
|SOAP 헤더|Description|  
|-----------------|-----------------|  
|BeginSession|이 헤더는 공급자에게 새 세션을 만들도록 요청합니다. 공급자는 새 세션을 생성한 후 SOAP 응답에 있는 세션 헤더의 일부로 세션 ID를 반환하여 응답해야 합니다.|  
|SessionId|값 영역에는 세션의 나머지 부분에서 각 메서드 호출에 사용해야 하는 세션 ID가 포함됩니다. SOAP 응답에 있는 공급자가 이 태그를 보내며 클라이언트도 이 특성을 각 세션 헤더 요소와 함께 보내야 합니다.|  
|Session|세션에서 발생한 모든 메서드 호출에서 이 헤더를 사용해야 하며 세션 ID가 헤더의 값 영역에 포함되어야 합니다.|  
|EndSession|세션을 종료하려면 이 헤더를 사용합니다. 세션 ID가 값 영역과 함께 포함되어야 합니다.|  
  
> [!NOTE]  
>  세션 ID는 세션이 유효한 상태를 유지함을 보장하지는 않습니다. 세션이 만료된 경우(예를 들어, 세션의 시간이 초과되거나 연결이 끊어진 경우) 공급자는 해당 세션의 동작을 종료하고 롤백할 수 있습니다. 결과적으로 세션 ID에 대한 클라이언트의 모든 후속 메서드 호출은 세션이 유효하지 않음을 나타내는 오류가 발생하면서 실패합니다. 클라이언트는 이 조건을 처리해야 하며 세션 메서드 호출을 처음부터 다시 보낼 준비를 해야 합니다.  
  
## <a name="legacy-code-example"></a>레거시 예제 코드  
 다음 예제에서는 세션이 지원되는 방법을 보여 줍니다.  
  
1.  세션을 시작하기 위해 SOAP의 BeginSession 헤더를 클라이언트의 아웃바운드 XMLA 메서드 호출에 추가합니다. 처음에는 세션 ID를 알지 못하므로 값 영역이 비어 있습니다.  
  
    ```  
    <SOAP-ENV:Envelope  
       xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
       SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
       <SOAP-ENV:Header>  
          <XA:BeginSession  
             xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
             xsi:type="xsd:int"  
             mustUnderstand="1"/>  
       </SOAP-ENV:Header>  
       <SOAP-ENV:Body>  
          ...<!-- Discover or Execute call goes here.-->  
       </SOAP-ENV:Body>  
    </SOAP-ENV:Envelope>  
    ```  
  
2.  공급자의 SOAP 응답 메시지에 포함 되어 세션 ID가 반환 헤더 영역에는 XMLA 헤더 태그를 사용 하 여 \<SessionId > 합니다.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
3.  세션의 각 메서드 호출에는 공급자가 반환한 세션 ID가 포함된 세션 헤더가 추가되어야 합니다.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
4.  세션이 완료 되 면는 \<EndSession > 관련된 세션 ID 값이 포함 된 태그가 사용 됩니다.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:EndSession  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          xsi:type="xsd:int"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

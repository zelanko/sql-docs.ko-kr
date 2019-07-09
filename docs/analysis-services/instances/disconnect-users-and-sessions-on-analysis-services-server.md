---
title: 사용자 연결 끊기에 Analysis Services 서버와 세션 | Microsoft Docs
ms.date: 07/05/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 696c6548dadda2412566acf7fae1e2cff2b28095
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624390"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Analysis Services 서버에서 사용자와 세션 연결 끊기
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  관리자로 서 워크 로드 관리의 일환으로 최종 사용자 작업 하는 것이 좋습니다. 사용자 작업을 종료하려면 세션 및 연결을 취소합니다. 세션은 쿼리 실행 시(암시적) 또는 관리자가 쿼리 생성 시 이름을 지정하면(명시적) 자동으로 구성될 수 있습니다. 연결은 쿼리를 실행할 수 있는 열린 통로입니다. 세션과 연결 모두 활성 상태에서 종료할 수 있습니다. 예를 들어, 다음 처리 시간이 너무 오래 실행 중인 명령이 올바르게 작성 되었다는 여부에 대 한 몇 가지 확실 하지 않은 우위에 아니면 세션에 대 한 처리를 종료 하는 것이 좋습니다.  
  
## <a name="ending-sessions-and-connections"></a>세션 및 연결 종료  
 세션 및 연결을 관리 하려면 동적 관리 뷰 (Dmv) 및 XMLA를 사용 합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 Analysis Services 인스턴스에 연결합니다.  
  
2.  MDX 쿼리 창에 다음 DMV 쿼리 중 하나를 붙여넣어 현재 실행 중인 모든 세션, 연결 및 명령 목록을 가져옵니다.  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  (이 쿼리 Azure Analysis Services에는 적용 되지 않습니다)
  
     `Select * from $System.Discover_Commands`  
  
3.  F5 키를 눌러 쿼리를 실행합니다.  
  
     DMV 쿼리는 읽고 복사하기 쉬운 테이블 형식의 결과 집합으로 세션 및 연결 정보를 반환합니다.  
  
 쿼리 창을 계속 열어 둡니다. 다음 단계에서 이 페이지로 돌아와 연결을 끊으려는 세션의 SPID를 복사해야 합니다.  
  
 세션을 종료하려면 두 번째 XMLA 쿼리 창을 엽니다.  
  
1.  MDX 쿼리 창에 다음 구문을 붙여넣고 ConnectionID, SessionID 또는 SPID 자리 표시자를 이전 단계에서 복사한 올바른 값으로 바꿉니다.  
  
    ```  
    <Cancel xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  
       <ConnectionID>111</ConnectionID>  
       <SessionID>222</SessionID>  
       <SPID>333</SPID>  
  
    <CancelAssociated>1</CancelAssociated>  
    </Cancel>  
  
    ```  
  
2.  F5 키를 눌러 취소 명령을 실행합니다.  

SPID/SessionID를 취소 하면 SPID 세션 Id를 해당 세션에서 실행 중인 모든 활성 명령이 취소 됩니다. 연결을 취소 연결에 연관 된 세션을 식별 하 고 해당 세션에서 실행 중인 모든 활성 명령이 취소 됩니다. 드문 경우에는 연결이 끊어지지 않은 모든 세션과 Spid; 연결과 관련 된 엔진을 추적할 수 없는 경우 예를 들어, 여러 세션이 있는 경우 HTTP 시나리오에서 엽니다.   
  
이 항목에서 참조 하는 XMLA에 대 한 자세한 내용은 참조 하세요 [메서드 실행 &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 하 고 [Cancel 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla).  
  
## <a name="see-also"></a>관련 항목  
 [연결 및 세션 관리&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [BeginSession 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [EndSession 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Session 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  

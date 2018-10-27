---
title: 사용자 연결 끊기에 Analysis Services 서버와 세션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ending user activity [Analysis Services]
- connections [Analysis Services]
- sessions [Analysis Services]
ms.assetid: 3b0145a2-f21d-4dd0-a09e-83afeb2ff4a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c451111875b2e1a638f49ad710b7456d3ba5eb17
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148448"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Analysis Services 서버에서 사용자와 세션 연결 끊기
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 관리자는 작업 관리 중에 사용자 작업을 종료할 수 있습니다. 사용자 작업을 종료하려면 세션 및 연결을 취소합니다. 세션은 쿼리 실행 시(암시적) 또는 관리자가 쿼리 생성 시 이름을 지정하면(명시적) 자동으로 구성될 수 있습니다. 연결은 쿼리를 실행할 수 있는 열린 통로입니다. 세션과 연결 모두 활성 상태에서 종료할 수 있습니다. 예를 들어 관리자는 처리 시간이 너무 오래 걸리거나 실행 중인 명령이 올바르게 작성되었다는 확신이 없을 경우 세션 처리를 종료할 수 있습니다.  
  
## <a name="ending-sessions-and-connections"></a>세션 및 연결 종료  
 DMV(동적 관리 뷰) 및 XMLA를 사용하여 세션 및 연결을 관리할 수 있습니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 Analysis Services 인스턴스에 연결합니다.  
  
2.  MDX 쿼리 창에 다음 DMV 쿼리 중 하나를 붙여넣어 현재 실행 중인 모든 세션, 연결 및 명령 목록을 가져옵니다.  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  
  
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
  
 연결을 종료하면 호스트 세션이 닫히면서 모든 세션과 SPID가 취소됩니다.  
  
 세션을 종료하면 해당 세션의 일부로 실행 중인 모든 명령(SPID)이 중지됩니다.  
  
 SPID를 종료하면 특정 명령이 취소됩니다.  
  
 아주 드물게는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 연결과 관련된 모든 세션 및 SPID를 추적할 수 없는 경우(예: HTTP 시나리오에서 여러 개의 세션이 열려 있는 경우) 이 연결을 닫지 않습니다.  
  
 이 항목에서 참조하는 XMLA에 대한 자세한 내용은 [Execute 메서드&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 및 [Cancel 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [연결 및 세션 관리&#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [BeginSession 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [EndSession 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Session 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  

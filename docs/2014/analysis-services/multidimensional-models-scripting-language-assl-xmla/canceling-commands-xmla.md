---
title: 명령 취소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80bddac8f800c1b9394c1ed605007ab0f2137b88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727467"
---
# <a name="canceling-commands-xmla"></a>명령 취소(XMLA)
  명령을 실행 하는 사용자의 관리 권한에 따라 XMLA (XML for Analysis)의 [Cancel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) 명령은 세션, 세션, 연결, 서버 프로세스 또는 연결 된 세션 또는 연결에서 명령을 취소할 수 있습니다.  
  
## <a name="canceling-commands"></a>명령 취소  
 사용자는 속성을 지정하지 않고 `Cancel` 명령을 보내어 현재 명시적 세션의 컨텍스트 내에서 현재 실행 중인 명령을 취소할 수 있습니다.  
  
> [!NOTE]  
>  암시적 세션에서 실행 중인 명령은 사용자가 취소할 수 없습니다.  
  
### <a name="canceling-batch-commands"></a>Batch 명령 취소  
 사용자가 `Batch` 명령을 취소하면 `Batch` 명령 내에서 아직 실행되지 않고 남아 있는 모든 명령이 취소됩니다. 
  `Batch` 명령이 트랜잭션인 경우 `Cancel` 명령이 실행되기 전에 실행된 모든 명령은 롤백됩니다.  
  
## <a name="canceling-sessions"></a>세션 취소  
 명령의 SessionID 속성에 명시적 세션에 대 한 세션 식별자를 지정 하 여 데이터베이스 관리자나 서버 관리자는 현재 실행 중인 명령을 포함 하 여 세션을 취소할 수 있습니다. [](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) `Cancel` 데이터베이스 관리자는 자신이 관리 권한을 가지고 있는 데이터베이스에 대한 세션만을 취소할 수 있습니다.  
  
 데이터베이스 관리자는 DISCOVER_SESSIONS 스키마 행 집합을 검색하여 지정된 데이터베이스의 활성 세션을 검색할 수 있습니다. DISCOVER_SESSIONS 스키마 행 집합을 검색 하기 위해 데이터베이스 관리자는 XMLA `Discover` 메서드를 사용 하 고 `Discover` 메서드의 restriction 속성에 있는 SESSION_CURRENT_DATABASE restriction 열에 대해 [](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla) 적절 한 데이터베이스 식별자를 지정 합니다.  
  
## <a name="canceling-connections"></a>연결 취소  
 서버 관리자는 `Cancel` 명령의 [ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla) 속성에 연결 식별자를 지정 하 여 실행 중인 모든 명령을 포함 하 여 지정 된 연결과 관련 된 모든 세션을 취소 하 고 연결을 취소할 수 있습니다.  
  
> [!NOTE]  
>  HTTP 연결을 제공 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 하는 동안 데이터 펌프가 여러 세션을 여는 경우와 같이 인스턴스에서 연결에 연결 된 세션을 찾아 취소할 수 없는 경우 해당 인스턴스는 연결을 취소할 수 없습니다. 
  `Cancel` 명령을 실행하는 동안 이런 경우가 발생하면 오류가 발생합니다.  
  
 서버 관리자는 XMLA [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 메서드를 통해 DISCOVER_CONNECTIONS 스키마 행 집합을 검색하여 `Discover` 인스턴스의 활성 세션을 검색할 수 있습니다.  
  
## <a name="canceling-server-processes"></a>서버 프로세스 취소  
 명령의 Spid 속성에서 SPID (서버 프로세스 식별자)를 지정 하면 서버 관리자가 지정 된 SPID와 연결 된 명령을 취소할 수 있습니다. [](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) `Cancel`  
  
## <a name="canceling-associated-sessions-and-connections"></a>연관된 세션 및 연결 취소  
 [Cancelassociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla) 속성을 true로 설정 하 여 `Cancel` 명령에 지정 된 연결, 세션 또는 SPID와 연결 된 연결, 세션 및 명령을 취소할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XMLA&#41;&#40;메서드를 검색 합니다.](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  

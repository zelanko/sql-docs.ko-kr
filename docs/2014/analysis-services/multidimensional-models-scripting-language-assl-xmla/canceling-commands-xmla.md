---
title: 명령 취소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5129dd84cdd120b778fb55986374d27055b5904c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081690"
---
# <a name="canceling-commands-xmla"></a>명령 취소(XMLA)
  명령을 실행 하는 사용자의 관리 권한에 따라는 [취소](../xmla/xml-elements-commands/cancel-element-xmla.md) Analysis (XMLA) 세션, 세션, 연결, 서버 프로세스 또는 연관된 된 세션이 명령을 취소할 수에 대 한 xml에서 명령 또는 연결입니다.  
  
## <a name="canceling-commands"></a>명령 취소  
 사용자는 속성을 지정하지 않고 `Cancel` 명령을 보내어 현재 명시적 세션의 컨텍스트 내에서 현재 실행 중인 명령을 취소할 수 있습니다.  
  
> [!NOTE]  
>  암시적 세션에서 실행 중인 명령은 사용자가 취소할 수 없습니다.  
  
### <a name="canceling-batch-commands"></a>Batch 명령 취소  
 사용자가 `Batch` 명령을 취소하면 `Batch` 명령 내에서 아직 실행되지 않고 남아 있는 모든 명령이 취소됩니다. `Batch` 명령이 트랜잭션인 경우 `Cancel` 명령이 실행되기 전에 실행된 모든 명령은 롤백됩니다.  
  
## <a name="canceling-sessions"></a>세션 취소  
 에 명시적 세션의 세션 식별자를 지정 하 여는 [SessionID](../xmla/xml-elements-properties/id-element-xmla.md) 의 속성은 `Cancel` 데이터베이스 관리자나 서버 관리자는 현재 실행 중인 명령을 포함 하 여 세션을 취소할 수 있습니다 . 데이터베이스 관리자는 자신이 관리 권한을 가지고 있는 데이터베이스에 대한 세션만을 취소할 수 있습니다.  
  
 데이터베이스 관리자는 DISCOVER_SESSIONS 스키마 행 집합을 검색하여 지정된 데이터베이스의 활성 세션을 검색할 수 있습니다. DISCOVER_SESSIONS 스키마 행 집합을 검색 하려면 데이터베이스 관리자가 사용 하 여 XMLA `Discover` 메서드에 SESSION_CURRENT_DATABASE 제한 열에 대 한 적절 한 데이터베이스 식별자를 지정 하 고는 [제한사항](../xmla/xml-elements-properties/restrictions-element-xmla.md) 의 속성은 `Discover` 메서드.  
  
## <a name="canceling-connections"></a>연결 취소  
 에 연결 식별자를 지정 하 여는 [ConnectionID](../xmla/xml-elements-properties/connectionid-element-xmla.md) 의 속성은 `Cancel` 서버 관리자의 모든 실행 중인 모든 명령을 포함 하 여 지정된 된 연결와 연결 된 세션을 취소할 수 있습니다 및 취소 하 고 연결 합니다.  
  
> [!NOTE]  
>  경우 인스턴스의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 찾아 인스턴스 연결을 취소할 수 없습니다 데이터 펌프가 여러 세션 HTTP 연결을 제공 하는 동안 때와 같은 연결을 통해 연결 된 세션을 취소할 수 없습니다. `Cancel` 명령을 실행하는 동안 이런 경우가 발생하면 오류가 발생합니다.  
  
 서버 관리자는 XMLA `Discover` 메서드를 통해 DISCOVER_CONNECTIONS 스키마 행 집합을 검색하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 활성 세션을 검색할 수 있습니다.  
  
## <a name="canceling-server-processes"></a>서버 프로세스 취소  
 서버 프로세스 식별자 (SPID)를 지정 하 여는 [SPID](../xmla/xml-elements-properties/spid-element-xmla.md) 의 속성은 `Cancel` 서버 관리자에 지정된 된 SPID에 연관 된 명령을 취소할 수 있습니다.  
  
## <a name="canceling-associated-sessions-and-connections"></a>연관된 세션 및 연결 취소  
 설정할 수 있습니다는 [CancelAssociated](../xmla/xml-elements-properties/cancelassociated-element-xmla.md) 속성을 true로 연결, 세션 및 연결 된 연결, 세션 또는 SPID에 지정 된 명령을 취소 하는 `Cancel` 명령입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Discover 메서드 &#40;XMLA&#41;](../xmla/xml-elements-methods-discover.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
---
title: MSSQLSERVER_2518 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f40eb8fe404479f5a2bcd68881aec4b2b2d84613
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091077"
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2518|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|메시지 텍스트|개체 ID O_ID(개체 "O_NAME"): CLR(공용 언어 런타임)을 사용할 수 없으므로 이 개체에 대해 계산 열과 사용자 정의 유형을 확인할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 이 정보 메시지는 쿼리 프로세서가 내부 개체와 DBCC를 제공할 수 없어 계산 열과 CLR(공통 언어 런타임) 사용자 정의 유형을 평가할 수 없음을 나타냅니다. 이 문제는 열 중 하나가 CLR과 관련되어 있으나 CLR을 사용할 수 없으므로 발생합니다. 내부 개체는 모든 열을 포함하므로 단일 열을 평가할 수 없으면 내부 개체를 생성할 수 없습니다. 따라서 계산 열이 올바른지 확인할 수 없으며 DBCC에서 인덱스와 기본 테이블 간의 일관성을 확인할 때 계산 열을 사용할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 CLR을 사용하고 DBCC 문을 다시 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 통합 사용](../clr-integration/clr-integration-enabling.md)  
  
  
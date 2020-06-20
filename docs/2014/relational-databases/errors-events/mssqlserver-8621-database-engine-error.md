---
title: MSSQLSERVER_8621 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8621 (Database Engine error)
ms.assetid: 67f59865-becd-4999-8bb0-90aedd7effbf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e054232776435a5d7825427393e6fbfa0bf232d6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053559"
---
# <a name="mssqlserver_8621"></a>MSSQLSERVER_8621
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8621|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|OPTIMIZER_STACK_OVERFLOW_ERR|  
|메시지 텍스트|쿼리 최적화 중 쿼리 프로세서에 스택 공간이 부족합니다. 쿼리를 단순하게 만드십시오.|  
  
## <a name="explanation"></a>설명  
 확장된 쿼리의 크기가 오류의 원인일 가능성이 높습니다. 확장된 쿼리는 보조 인덱스 및 뷰의 업데이트나 트리거와 같은 연계 동작은 물론 각 뷰, 계산 열, [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수 및 참조하는 공통 테이블 식 등의 정의로 원래 쿼리를 대체합니다.  
  
 쿼리의 특정 수치가 너무 크기 때문일 가능성이 높습니다. 예를 들어 뷰 정의에서 참조하는 테이블의 수가 지나치게 많거나 스칼라 식이 너무 크기 때문일 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 가장 큰 수치를 기준으로 쿼리를 여러 개로 나누어 단순하게 만듭니다. 먼저 불필요한 쿼리 요소를 제거한 후 임시 테이블을 추가하고 쿼리를 두 개로 분할합니다.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 컴파일러가 이들을 다시 결합하므로 단지 쿼리의 일부를 하위 쿼리, 함수 또는 공통 테이블 식으로 옮기는 것만으로는 부족합니다.  
  
  

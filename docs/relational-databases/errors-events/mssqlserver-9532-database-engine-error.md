---
title: "MSSQLSERVER_9532 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8c88ac3f700fa2f91a868f7a7fb1590d4119d0cc
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9532"></a>MSSQLSERVER_9532
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|9532|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|메시지 텍스트|열 집합 '%.*ls'이(가) 관련된 쿼리/DML 작업 시 열 '%.\*ls'의 데이터 형식 '%ls'을(를) 데이터 형식 '%ls'(으)로 변환하지 못했습니다.|  
  
## <a name="explanation"></a>설명  
열 집합은 일부 테이블 열을 구조화된 출력으로 결합하는 형식화되지 않은 XML 표현입니다. XML 열 집합 통해 스파스 열 값을 삽입하거나 업데이트하는 경우 기본 스파스 열에 삽입된 값은 **xml** 데이터 형식에서 암시적으로 변환됩니다. 열 데이터 형식으로 변환할 수 없는 값을 제공했습니다.  
  
## <a name="user-action"></a>사용자 동작  
제공된 값을 암시적으로 변환할 수 없으므로 잘못 입력한 것 같습니다. 오류를 수정하고 다시 시도합니다. 값이 올바른 경우 열 집합 대신 개별 열을 사용하도록 문을 수정합니다. 그러면 값을 올바른 데이터 형식으로 명시적으로 캐스팅할 수 있습니다.  
  


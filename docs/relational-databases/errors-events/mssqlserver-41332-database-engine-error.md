---
title: MSSQLSERVER_41332 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1110d388e5f9459526cd47d80b5ebc2907c5df94
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68123308"
---
# <a name="mssqlserver_41332"></a>MSSQLSERVER_41332
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41332|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQL_SNAPSHOT_NOT_SUPPORTED|  
|메시지 텍스트|TRANSACTION ISOLATION LEVEL 세션을 SNAPSHOT으로 설정하면 메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저에 액세스하거나 만들 수 없습니다.|  
  
## <a name="explanation"></a>설명  
트랜잭션이 스냅샷 격리 수준에서 시작된 다음 호환되지 않는 기능을 사용하려고 했습니다.  
  
## <a name="user-action"></a>사용자 동작  
다른 격리 수준으로 트랜잭션을 시작합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

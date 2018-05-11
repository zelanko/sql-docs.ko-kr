---
title: MSSQLSERVER_41302 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 41302 (Database Engine error)
ms.assetid: 01e75618-afec-4232-ba68-93ab7bc31003
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f64069b75975de1ae58acf73299e902ebbbeef1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver41302"></a>MSSQLSERVER_41302
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41302|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|WRITE_WRITE_CONFLICT|  
|메시지 텍스트|현재 트랜잭션이 시작된 이후에 업데이트된 레코드를 업데이트하려고 시도했습니다. 트랜잭션이 중단되었습니다.|  
  
## <a name="explanation"></a>설명  
트랜잭션에서 쓰기/쓰기 충돌이 발생하여 문이 종료되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
나중에 다른 트랜잭션에서 작업을 다시 시도합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

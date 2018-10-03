---
title: MSSQLSERVER_41302 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41302 (Database Engine error)
ms.assetid: 01e75618-afec-4232-ba68-93ab7bc31003
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2808c76867092777a50cd56b917b8431e5dabe2a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205193"
---
# <a name="mssqlserver41302"></a>MSSQLSERVER_41302
    
## <a name="details"></a>설명  
  
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
 나중에 다른 트랜잭션에서 작업을 다시 시도합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

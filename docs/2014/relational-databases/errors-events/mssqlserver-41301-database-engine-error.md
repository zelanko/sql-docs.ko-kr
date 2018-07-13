---
title: MSSQLSERVER_41301 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41301 (Database Engine error)
ms.assetid: c6127e1e-2846-4ee9-bc42-2d896ea9730e
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9281a679d49329faaee903dd1549c07e5dd88449
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37418782"
---
# <a name="mssqlserver41301"></a>MSSQLSERVER_41301
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41301|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|COMMIT_DEPENDENCY_FAILURE|  
|메시지 텍스트|현재 트랜잭션이 종속성을 갖고 있는 이전 트랜잭션이 중단되어 현재 트랜잭션을 더 이상 커밋할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 종속성 오류가 발생하여 트랜잭션을 종료합니다.  
  
 종속 트랜잭션이 너무 많아도 이 오류가 발생할 수 있습니다. 모든 쓰기 트랜잭션은 제한된 수의 종속 트랜잭션을 가질 수 있습니다. 예를 들어, 너무 많은 읽기 트랜잭션에서 업데이트 트랜잭션에 대한 종속성을 가지려고 할 경우 이 오류가 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 트랜잭션에서 어떤 작업도 수행하지 않습니다. ROLLBACK TRAN을 호출하여 트랜잭션을 롤백합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
  

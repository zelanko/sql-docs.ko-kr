---
title: MSSQLSERVER_41332 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0bbd8b256145a9d91e8615aaf7d87a4b8ce7b8b7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211563"
---
# <a name="mssqlserver41332"></a>MSSQLSERVER_41332
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41332|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQL_SNAPSHOT_NOT_SUPPORTED|  
|메시지 텍스트|TRANSACTION ISOLATION LEVEL 세션을 SNAPSHOT으로 설정하면 메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저에 액세스하거나 만들 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 트랜잭션이 스냅숏 격리 수준에서 시작된 다음 호환되지 않는 기능을 사용하려고 했습니다.  
  
## <a name="user-action"></a>사용자 동작  
 다른 격리 수준으로 트랜잭션을 시작합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

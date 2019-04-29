---
title: MSSQLSERVER_41325 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41325 (Database Engine error)
ms.assetid: 97c6a8bb-139a-44f3-9ed5-f46d047e8ed3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c78044f8790f3a1ab97d036467813efa3d30e6b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913999"
---
# <a name="mssqlserver41325"></a>MSSQLSERVER_41325
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41325|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HK_TX_COMMIT_SR_VALIDATION|  
|메시지 텍스트|직렬화 유효성 검사 실패로 인해 현재 트랜잭션을 커밋하지 못했습니다.|  
  
## <a name="explanation"></a>설명  
 유효성 검사 오류가 발생하여 트랜잭션을 종료합니다.  
  
## <a name="user-action"></a>사용자 동작  
 실패한 트랜잭션을 다시 시도합니다. 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

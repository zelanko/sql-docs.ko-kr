---
title: MSSQLSERVER_17084 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f410856e3be5f7d80acda994cc7eab0ad8e477be
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553688"
---
# <a name="mssqlserver_17084"></a>MSSQLSERVER_17084
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|17084|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|P3_ATOMIC_WITH_MISSING_OPTION|  
|메시지 텍스트|BEGIN ATOMIC 문의 WITH 절은 '%ls' 옵션에 대한 값을 지정해야 합니다.|  
  
## <a name="explanation"></a>설명  
 BEGIN ATOMIC 문의 WITH 절이 옵션 값을 지정하지 않았습니다.  
  
## <a name="user-action"></a>사용자 동작  
 `ATOMIC` 블록에는 `WITH` 옵션 `TRANSACTION ISOLATION LEVEL` 및 `LANGUAGE`에 대한 값이 필요합니다. 예::  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

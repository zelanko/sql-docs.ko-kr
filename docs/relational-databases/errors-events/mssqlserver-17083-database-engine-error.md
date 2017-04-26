---
title: "MSSQLSERVER_17083 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17083 (Database Engine error)
ms.assetid: 6c83737d-0531-4fd9-88f6-2da5a150532d
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea00cdd0a53e1db30e22a36815357e02e4a56485
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver17083"></a>MSSQLSERVER_17083
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|17083|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|P3_HEKATON_NOT_ATOMIC|  
|메시지 텍스트|고유하게 컴파일된 저장 프로시저의 본문은 ATOMIC 블록이어야 합니다.|  
  
## <a name="explanation"></a>설명  
고유하게 컴파일된 저장 프로시저의 본문에 ATOMIC 블록이 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
고유하게 컴파일된 저장 프로시저의 본문에는 ATOMIC 블록이 있어야 합니다. 예를 들어  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N’us_english’)  
```  
  
자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  


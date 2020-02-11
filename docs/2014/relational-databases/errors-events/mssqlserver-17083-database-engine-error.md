---
title: MSSQLSERVER_17083 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17083 (Database Engine error)
ms.assetid: 6c83737d-0531-4fd9-88f6-2da5a150532d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c04d010a690d99d90ea3a18ae7f70d33ed39f24b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915500"
---
# <a name="mssqlserver_17083"></a>MSSQLSERVER_17083
    
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
 고유하게 컴파일된 저장 프로시저의 본문에는 ATOMIC 블록이 있어야 합니다. 다음은 그 예입니다.  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

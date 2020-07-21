---
title: MSSQLSERVER_12304 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4649a51e0cd8842fe4e96e9a07b095091d04d4ed
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553848"
---
# <a name="mssqlserver_12304"></a>MSSQLSERVER_12304
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|12304|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|메시지 텍스트|열에서 IDENTITY 속성을 사용하는 메모리 액세스에 최적화된 테이블의 사용은 고유하게 컴파일된 저장 프로시저의 컨텍스트 외부에 있는 형식을 사용할 때 지원되지 않습니다.|  
  
## <a name="user-action"></a>사용자 동작  
 열에서 IDENTITY 속성을 사용하는 메모리 최적화 테이블 형식을 사용하지 마세요.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

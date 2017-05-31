---
title: "MSSQLSERVER_12329 | Microsoft 문서"
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
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
caps.latest.revision: 4
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 47b2380fdb3bf5fbde95bfbd984c3ed6095dcd1f
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|12329|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HK_UNSUPPORTED_NON_LATIN_CODEPAGE|  
|메시지 텍스트|1252가 아닌 코드 페이지가 있는 데이터 정렬을 사용하는 데이터 형식 char(n) 및 varchar(n)는 *construct*에서 지원되지 않습니다.|  
  
## <a name="explanation"></a>설명  
1252가 아닌 코드 페이지가 있는 데이터 정렬을 사용하는 데이터 형식 char(n) 및 varchar(n)를 사용하지 마십시오.  
  
## <a name="user-action"></a>사용자 동작  
이 오류를 발생시킬 수 있는 예기치 않은 한 가지 상황은 다음과 같습니다.  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
대신 다음을 사용하십시오.  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  


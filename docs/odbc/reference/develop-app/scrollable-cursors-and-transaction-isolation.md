---
title: "스크롤 가능 커서 및 트랜잭션 격리 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6c9e38f4287a8832d8e794940093ce696ac0eaf7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>스크롤 가능 커서 및 트랜잭션 격리
다음 표에서 변경 내용 표시를 제어 하는 요소를 나열 합니다.  
  
|수행한 변경 내용:|표시 여부에 따라 달라 집니다.|  
|----------------------|----------------------------|  
|커서|커서 유형, 커서 구현|  
|동일한 트랜잭션에서 다른 문|커서 유형|  
|다른 트랜잭션의 문|트랜잭션 격리 수준 커서 유형|  
  
 이러한 요소는 다음 그림에 표시 됩니다.  
  
 ![변경 내용 표시를 제어 하는 요인](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 다음 표에서 자체적으로, 자체 트랜잭션에서 특정 작업 및 다른 트랜잭션에서 변경한 내용을 검색 하는 각 커서 유형의 기능을 요약 합니다. 두 번째 변경 내용 표시 커서 유형과 커서가 포함 된 트랜잭션 격리 수준에 따라 달라 집니다.  
  
|커서 type\action|자체|소유<br /><br /> Txn|기타<br /><br /> Txn<br /><br /> (RU[a])|기타<br /><br /> Txn<br /><br /> (RC[a])|기타<br /><br /> Txn<br /><br /> (RR[a])|기타<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|정적|||||||  
|Insert|Maybe [b]|아니오|아니오|아니오|아니오|아니오|  
|Update|Maybe [b]|아니오|아니오|아니오|아니오|아니오|  
|DELETE|Maybe [b]|아니오|아니오|아니오|아니오|아니오|  
|키 집합|||||||  
|Insert|Maybe [b]|아니오|아니오|아니오|아니오|아니오|  
|Update|예|예|예|예|아니오|아니오|  
|DELETE|Maybe [b]|예|예|예|아니오|아니오|  
|Dynamic|||||||  
|Insert|예|예|예|예|예|아니오|  
|Update|예|예|예|예|아니오|아니오|  
|DELETE|예|예|예|예|아니오|아니오|  
  
 [a] 괄호로 문자 나타냅니다는 커서를 포함 하는 트랜잭션의 격리 수준 (에 변경) 다른 트랜잭션 격리 수준을 관련이 없습니다.  
  
 커밋되지 않은 RU: 읽기  
  
 Read committed에 RC의 경우:  
  
 RR: 반복 읽기  
  
 직렬화 가능 s:  
  
 [b]는 커서를 구현 하는 방법에 따라 달라 집니다. SQL_STATIC_SENSITIVITY 옵션을 통해 보고 되는 커서가 이러한 변경 내용을 검색할 수 있는지 여부 **SQLGetInfo**합니다.

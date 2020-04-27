---
title: 문 핸들 해제 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b1a155f7d2ee6cc5f92d46c2bb744168dc5ebc0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63200052"
---
# <a name="freeing-a-statement-handle"></a>문 핸들 해제
  문 핸들을 다시 사용하는 것이 문 핸들을 삭제한 다음 새로 할당하는 것보다 더 효율적입니다. 따라서 문 핸들에 대해 새 SQL 문을 실행하기 전에 애플리케이션에서 현재 문 설정이 적절한지 확인해야 합니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 일반적으로 이전 SQL 문에 대 한 매개 변수 및 결과 집합은 SQL_RESET_PARAMS와 SQL_UNBIND 옵션을 사용 하 여 [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) 를 호출한 다음 새 SQL 문에 대해 다시 바인딩하여 바인딩 해제 해야 합니다.  
  
 응용 프로그램에서 문 사용을 마치면 [Sqlfreehandle](../native-client-odbc-api/sqlfreehandle.md) 을 호출 하 여 문을 해제 합니다. **Sqldisconnect** 는 연결에서 모든 문을 자동으로 해제 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;쿼리 실행](executing-queries-odbc.md)  
  
  

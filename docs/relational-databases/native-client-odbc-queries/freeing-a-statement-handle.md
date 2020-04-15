---
title: 명세서 핸들 해제 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e954773f85afc434d1e5bd18f7ffb76e28a1438
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297899"
---
# <a name="freeing-a-statement-handle"></a>문 핸들 해제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  문 핸들을 다시 사용하는 것이 문 핸들을 삭제한 다음 새로 할당하는 것보다 더 효율적입니다. 따라서 문 핸들에 대해 새 SQL 문을 실행하기 전에 애플리케이션에서 현재 문 설정이 적절한지 확인해야 합니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 일반적으로 이전 SQL 문에 대한 매개 변수 및 결과 집합은 SQL_RESET_PARAMS 및 SQL_UNBIND 옵션으로 [SQLFreeStmt를](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 호출한 다음 새 SQL 문에 다시 바인딩하여 바인딩되지 않아야 합니다.  
  
 응용 프로그램이 문을 사용하여 완료되면 [SQLFreeHandle을](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 호출하여 문을 해제합니다. **SQLDisconnect는** 연결의 모든 문을 자동으로 해제합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;쿼리 실행](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  

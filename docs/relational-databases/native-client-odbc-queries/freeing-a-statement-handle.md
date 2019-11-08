---
title: 문 핸들 해제 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 405e5fd13298892a2c6226015f575ef9b8373148
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779423"
---
# <a name="freeing-a-statement-handle"></a>문 핸들 해제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  문 핸들을 다시 사용하는 것이 문 핸들을 삭제한 다음 새로 할당하는 것보다 더 효율적입니다. 따라서 문 핸들에 대해 새 SQL 문을 실행하기 전에 애플리케이션에서 현재 문 설정이 적절한지 확인해야 합니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 일반적으로 이전 SQL 문에 대 한 매개 변수 및 결과 집합은 SQL_RESET_PARAMS와 SQL_UNBIND 옵션을 사용 하 여 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 를 호출한 다음 새 SQL 문에 대해 다시 바인딩하여 바인딩 해제 해야 합니다.  
  
 응용 프로그램에서 문 사용을 마치면 [Sqlfreehandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 을 호출 하 여 문을 해제 합니다. **Sqldisconnect** 는 연결에서 모든 문을 자동으로 해제 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 쿼리 &#40;실행&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  

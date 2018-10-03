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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1c28f3ba81ffbe346572dfba92adb31a7f198af9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47598701"
---
# <a name="freeing-a-statement-handle"></a>문 핸들 해제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  문 핸들을 다시 사용하는 것이 문 핸들을 삭제한 다음 새로 할당하는 것보다 더 효율적입니다. 따라서 문 핸들에 대해 새 SQL 문을 실행하기 전에 응용 프로그램에서 현재 문 설정이 적절한지 확인해야 합니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 매개 변수 및 결과 이전 SQL 문을 호출 하 여 바인딩 해제에 대 한 설정 하는 일반적으로 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) SQL_RESET_PARAMS 및 SQL_UNBIND 옵션 및 새 SQL 문에 대 한 다시 바인딩해야 합니다.  
  
 호출 응용 프로그램은 문을 사용 하 여 완료 되 면 [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 에 해당 문을 해제 합니다. 사실은 **SQLDisconnect** 자동으로 연결 된 모든 문을 해제 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 실행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  

---
description: 문의 일괄 처리
title: 문 일괄 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9d0842a0cc4c38c25af9dc3bdf334f846993f480
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867309"
---
# <a name="batches-of-statements"></a>문의 일괄 처리
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  문 일괄 처리에는 두 개 이상의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이 포함 되어 있습니다. 세미콜론 (;)은 **Sqlexecdirect** 또는 [sqlprepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)에 전달 된 단일 문자열로 기본 제공 됩니다. 예를 들면 다음과 같습니다.  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 일괄 처리를 사용하면 대개 네트워크 트래픽이 줄어들므로 문을 개별적으로 전송하는 것보다 효율적일 수 있습니다. [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 를 사용 하 여 현재 결과 집합을 마치면 다음 결과 집합에 배치 합니다.  
  
 ODBC 커서 특성을 행 집합 크기가 1인 정방향 전용의 읽기 전용 커서(기본값)로 설정하면 항상 일괄 처리를 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대해 서버 커서를 사용할 때 일괄 처리를 실행하면 서버 커서가 암시적으로 기본 결과 집합으로 변환됩니다. **Sqlexecdirect** 또는 **sqlexecute** 반환 SQL_SUCCESS_WITH_INFO, **SQLGetDiagRec** 에 대 한 호출은 다음을 반환 합니다.  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;문을 실행 하는 중 ](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  

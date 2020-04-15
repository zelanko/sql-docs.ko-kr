---
title: 저장 프로시저 호출 일괄 처리 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ef16b6c6b599274072bddfc49a58de2a10712ea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304569"
---
# <a name="batching-stored-procedure-calls"></a>저장 프로시저 호출 일괄 처리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 적절한 경우 저장된 프로시저 호출을 서버에 자동으로 일괄 처리합니다. 이 드라이버는 ODBC CALL 이스케이프 시퀀스가 사용된 경우에만 이러한 작업을 수행하고 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 문이 실행된 경우에는 수행하지 않습니다. 저장 프로시저 호출을 일괄 처리하면 서버 왕복 횟수가 줄어들고 성능이 대폭 향상됩니다.  
  
 여러 개의 ODBC CALL 이스케이프 시퀀스가 포함된 일괄 처리를 실행하면 드라이버가 서버에 대한 프로시저 호출을 일괄 처리합니다. 또한 드라이버는 ODBC CALL 이스케이프 시퀀스와 함께 바인딩된 매개 변수 배열이 사용된 경우에도 프로시저 호출을 일괄 처리합니다. 예를 들어 행 별 또는 열 별 매개 변수 바인딩을 사용하여 5개의 요소가 있는 배열을 ODBC CALL SQL 문의 매개 변수에 바인딩하는 경우 **SQLExecute** 또는 **SQLExecDirect가** 호출될 때 드라이버는 서버에 5개의 프로시저 호출이 있는 단일 일괄 처리를 보냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 실행](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  

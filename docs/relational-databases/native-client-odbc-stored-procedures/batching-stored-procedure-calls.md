---
title: 저장 프로시저 호출 일괄 처리 | Microsoft Docs
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
ms.openlocfilehash: c5d11da0c261619fdf3b133617dc2501a5e9532a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004644"
---
# <a name="batching-stored-procedure-calls"></a>저장 프로시저 호출 일괄 처리
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 적절 한 경우 서버에 대 한 저장 프로시저 호출을 자동으로 일괄 처리 합니다. 이 드라이버는 ODBC CALL 이스케이프 시퀀스가 사용된 경우에만 이러한 작업을 수행하고 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 문이 실행된 경우에는 수행하지 않습니다. 저장 프로시저 호출을 일괄 처리하면 서버 왕복 횟수가 줄어들고 성능이 대폭 향상됩니다.  
  
 여러 개의 ODBC CALL 이스케이프 시퀀스가 포함된 일괄 처리를 실행하면 드라이버가 서버에 대한 프로시저 호출을 일괄 처리합니다. 또한 드라이버는 ODBC CALL 이스케이프 시퀀스와 함께 바인딩된 매개 변수 배열이 사용된 경우에도 프로시저 호출을 일괄 처리합니다. 예를 들어 행 단위 또는 열 단위 매개 변수 바인딩을 사용 하 여 5 개의 요소가 포함 된 배열을 ODBC CALL SQL 문의 매개 변수에 바인딩하는 경우 **Sqlexecute** 또는 **sqlexecdirect** 를 호출 하면 드라이버에서 서버에 대 한 프로시저 호출이 5 개인 단일 일괄 처리를 보냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 실행](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  

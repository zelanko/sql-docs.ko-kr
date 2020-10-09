---
title: 저장 프로시저 호출 (ODBC) | Microsoft Docs
description: SQL Server 2005 이상에서 ODBC 응용 프로그램을 사용 하기 전에 ODBC 관리자를 사용 하 여 프로그래밍 방식으로 또는 파일을 사용 하 여 데이터 원본을 추가 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 76c5e2aab1f515ee52feb97218880e8831f3bea8
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868841"
---
# <a name="running-stored-procedures---call-stored-procedures"></a>저장 프로시저 실행 - 저장 프로시저 호출
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버를 사용하면 저장 프로시저를 원격 저장 프로시저로 실행할 수 있습니다. 저장 프로시저를 원격 저장 프로시저로 실행하면 드라이버와 서버에서 프로시저의 실행 성능을 최적화할 수 있습니다.  
  
  SQL 문이 ODBC CALL 이스케이프 절을 사용하여 저장 프로시저를 호출하는 경우 Microsoft® SQL Server™ 드라이버는 RPC(원격 저장 프로시저) 메커니즘을 사용하여 해당 프로시저를 SQL Server로 보냅니다. RPC 요청은 SQL Server의 문 구문 분석과 매개 변수 처리를 대부분 무시하므로 Transact-SQL EXECUTE 문을 사용할 때보다 속도가 향상됩니다.  
  
 이 기능을 보여 주는 예제 응용 프로그램은 [ODBC&#41;&#40;반환 코드 및 출력 매개 변수 처리 ](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md)를 참조 하세요.  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>프로시저를 RPC로 실행하려면  
  
1.  ODBC CALL 이스케이프 시퀀스를 사용하는 SQL 문을 생성합니다. 이 문에서는 각 입/출력 및 출력 매개 변수와 프로시저 반환 값(있는 경우)에 대해 매개 변수 표식을 사용합니다.  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  각 입력, 입/출력 및 출력 매개 변수와 프로시저 반환 값(있는 경우)에 대해 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 를 호출합니다.  
  
3.  [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md)를 사용하여 문을 실행합니다.  
  
> [!NOTE]  
>  애플리케이션이 ODBC CALL 이스케이프 시퀀스가 아닌 Transact-SQL EXECUTE 구문을 사용하여 프로시저를 제출하는 경우 SQL Server ODBC 드라이버는 프로시저 호출을 RPC 대신 SQL 문으로 SQL Server에 전달합니다. 또한 Transact-SQL EXECUTE 문을 사용하면 출력 매개 변수가 반환되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
  [저장 프로시저 호출 일괄 처리](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [저장 프로시저 실행](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [저장 프로시저 호출](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [절차](../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  

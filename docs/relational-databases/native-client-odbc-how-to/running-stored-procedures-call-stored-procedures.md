---
title: "저장된 프로시저 (ODBC) 호출 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e8aa0ae9c68313671e3d6e9c8ad1a71392f9524
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="running-stored-procedures---call-stored-procedures"></a>저장된 프로시저를 호출 하는 저장된 프로시저-실행
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버를 사용하면 저장 프로시저를 원격 저장 프로시저로 실행할 수 있습니다. 저장 프로시저를 원격 저장 프로시저로 실행하면 드라이버와 서버에서 프로시저의 실행 성능을 최적화할 수 있습니다.  
  
  SQL 문이 ODBC CALL 이스케이프 절을 사용하여 저장 프로시저를 호출하는 경우 Microsoft® SQL Server™ 드라이버는 RPC(원격 저장 프로시저) 메커니즘을 사용하여 해당 프로시저를 SQL Server로 보냅니다. RPC 요청은 SQL Server의 문 구문 분석과 매개 변수 처리를 대부분 무시하므로 Transact-SQL EXECUTE 문을 사용할 때보다 속도가 향상됩니다.  
  
 이 기능을 보여 주는 샘플 응용 프로그램을 참조 하십시오. [프로세스 반환 코드 및 출력 매개 변수 사용 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md)합니다.  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>프로시저를 RPC로 실행하려면  
  
1.  ODBC CALL 이스케이프 시퀀스를 사용하는 SQL 문을 생성합니다. 이 문에서는 각 입/출력 및 출력 매개 변수와 프로시저 반환 값(있는 경우)에 대해 매개 변수 표식을 사용합니다.  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  호출 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 각 입력에 대 한 입/출력 및 출력 매개 변수 및 프로시저에 대 한 반환 값 (있는 경우).  
  
3.  사용 하 여 문을 실행 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399)합니다.  
  
> [!NOTE]  
>  응용 프로그램이 ODBC CALL 이스케이프 시퀀스가 아닌 Transact-SQL EXECUTE 구문을 사용하여 프로시저를 제출하는 경우 SQL Server ODBC 드라이버는 프로시저 호출을 RPC 대신 SQL 문으로 SQL Server에 전달합니다. 또한 Transact-SQL EXECUTE 문을 사용하면 출력 매개 변수가 반환되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
  [일괄 처리 저장된 프로시저 호출](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [저장된 프로시저 실행](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [저장된 프로시저 호출](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [절차](../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
  

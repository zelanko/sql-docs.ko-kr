---
title: 저장된 프로시저 (ODBC) 호출 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0846567d803eadf4364159fc01fdb8a7853e8a4f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092204"
---
# <a name="call-stored-procedures-odbc"></a>저장 프로시저 호출(ODBC)
  SQL 문이 ODBC CALL 이스케이프 절을 사용하여 저장 프로시저를 호출하는 경우 Microsoft® SQL Server™ 드라이버는 RPC(원격 저장 프로시저) 메커니즘을 사용하여 해당 프로시저를 SQL Server로 보냅니다. RPC 요청은 SQL Server의 문 구문 분석과 매개 변수 처리를 대부분 무시하므로 Transact-SQL EXECUTE 문을 사용할 때보다 속도가 향상됩니다.  
  
 이 기능을 보여 주는 샘플 응용 프로그램을 참조 하십시오. [프로세스 반환 코드 및 출력 매개 변수 &#40;ODBC&#41;](running-stored-procedures-process-return-codes-and-output-parameters.md)합니다.  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>프로시저를 RPC로 실행하려면  
  
1.  ODBC CALL 이스케이프 시퀀스를 사용하는 SQL 문을 생성합니다. 이 문에서는 각 입/출력 및 출력 매개 변수와 프로시저 반환 값(있는 경우)에 대해 매개 변수 표식을 사용합니다.  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  호출 [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) 각 입력에 대 한 입/출력 및 출력 매개 변수 및 프로시저에 대 한 반환 값 (있는 경우).  
  
3.  사용 하 여 문을 실행 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399)합니다.  
  
> [!NOTE]  
>  응용 프로그램이 ODBC CALL 이스케이프 시퀀스가 아닌 Transact-SQL EXECUTE 구문을 사용하여 프로시저를 제출하는 경우 SQL Server ODBC 드라이버는 프로시저 호출을 RPC 대신 SQL 문으로 SQL Server에 전달합니다. 또한 Transact-SQL EXECUTE 문을 사용하면 출력 매개 변수가 반환되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [저장된 프로시저 방법 도움말 항목 실행 &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [일괄 처리 저장된 프로시저 호출](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [저장된 프로시저 실행](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [저장된 프로시저 호출](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [절차](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  
---
title: 저장된 프로시저 (ODBC)를 호출 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58e5160065847d5729548702b5f1d65eb31bf694
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200267"
---
# <a name="call-stored-procedures-odbc"></a>저장 프로시저 호출(ODBC)
  SQL 문이 ODBC CALL 이스케이프 절을 Microsoft를 사용 하 여 저장된 프로시저를 호출 하는 경우?? SQL Server??? 드라이버가 보냅니다 원격 저장된 프로시저 호출 (RPC) 메커니즘을 사용 하 여 SQL server 절차. RPC 요청은 SQL Server의 문 구문 분석과 매개 변수 처리를 대부분 무시하므로 Transact-SQL EXECUTE 문을 사용할 때보다 속도가 향상됩니다.  
  
 이 기능을 보여 주는 샘플 응용 프로그램을 참조 하세요 [프로세스 반환 코드 및 출력 매개 변수 &#40;ODBC&#41;](running-stored-procedures-process-return-codes-and-output-parameters.md)합니다.  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>프로시저를 RPC로 실행하려면  
  
1.  ODBC CALL 이스케이프 시퀀스를 사용하는 SQL 문을 생성합니다. 이 문에서는 각 입/출력 및 출력 매개 변수와 프로시저 반환 값(있는 경우)에 대해 매개 변수 표식을 사용합니다.  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  각 입력, 입/출력 및 출력 매개 변수와 프로시저 반환 값(있는 경우)에 대해 [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) 를 호출합니다.  
  
3.  [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)를 사용하여 문을 실행합니다.  
  
> [!NOTE]  
>  응용 프로그램이 ODBC CALL 이스케이프 시퀀스가 아닌 Transact-SQL EXECUTE 구문을 사용하여 프로시저를 제출하는 경우 SQL Server ODBC 드라이버는 프로시저 호출을 RPC 대신 SQL 문으로 SQL Server에 전달합니다. 또한 Transact-SQL EXECUTE 문을 사용하면 출력 매개 변수가 반환되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [저장된 프로시저 방법 도움말 항목을 실행 &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [저장된 프로시저 호출 일괄 처리](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [저장된 프로시저 실행](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [저장된 프로시저를 호출합니다.](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [절차](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  

---
title: 준비와 문 실행 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- statement execution
- statement preparation
ms.assetid: 0adecc63-4da5-486c-bc48-09a004a2fae6
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 58a3ecf2419f0b3e3b74ba6e3b1a6293d928d550
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181590"
---
# <a name="prepare-and-execute-a-statement-odbc"></a>문 준비 및 실행(ODBC)
    
### <a name="to-prepare-a-statement-once-and-then-execute-it-multiple-times"></a>문을 한 번 준비한 후 여러 번 실행하려면  
  
1.  [SQLPrepare 함수](http://go.microsoft.com/fwlink/?LinkId=59360) 를 호출하여 문을 준비합니다.  
  
2.  필요에 따라 [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) 를 호출하여 준비된 문의 매개 변수 수를 확인합니다.  
  
3.  필요에 따라 준비된 문의 각 매개 변수에 대해 다음 작업을 수행합니다.  
  
    -   호출 [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) 매개 변수 정보를 가져올 수 있습니다.  
  
    -   각 매개 변수를 사용 하 여 프로그램 변수에 바인딩합니다 [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md)합니다. 실행 시 데이터 매개 변수를 설정합니다.  
  
4.  준비된 문을 실행할 때마다 다음 작업을 수행합니다.  
  
    -   문에 매개 변수 표식이 있는 경우 데이터 값을 바인딩된 매개 변수 버퍼에 넣습니다.  
  
    -   [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) 를 호출하여 준비된 문을 실행합니다.  
  
    -   실행 시 데이터 입력 매개 변수를 사용하는 경우 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) 는 SQL_NEED_DATA를 반환합니다. 사용 하 여 데이터를 청크로 보냅니다 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=58405) 및 [SQLPutData](../../native-client-odbc-api/sqlputdata.md)합니다.  
  
### <a name="to-prepare-a-statement-with-column-wise-parameter-binding"></a>열 단위 매개 변수 바인딩을 사용하여 문을 준비하려면  
  
1.  [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) 을 호출하여 다음 특성을 설정합니다.  
  
    -   SQL_ATTR_PARAMSET_SIZE를 매개 변수 집합 수(S)로 설정합니다.  
  
    -   SQL_ATTR_PARAM_BIND_TYPE을 SQL_PARAMETER_BIND_BY_COLUMN으로 설정합니다.  
  
    -   SQL_ATTR_PARAMS_PROCESSED_PTR 특성을 처리된 매개 변수 수를 보유하는 SQLUINTEGER 변수를 가리키도록 설정합니다.  
  
    -   SQL_ATTR_PARAMS_STATUS_PTR을 매개 변수 상태 표시를 보유하는 SQLUSSMALLINT 변수의 배열[S]을 가리키도록 설정합니다.  
  
2.  SQLPrepare에서 문 준비를 호출 합니다.  
  
3.  필요에 따라 [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) 를 호출하여 준비된 문의 매개 변수 수를 확인합니다.  
  
4.  필요에 따라 준비 된 문의 각 매개 변수에 대해 매개 변수 정보를 얻으려면 SQLDescribeParam를 호출 합니다.  
  
5.  각 매개 변수 표식에 대해 다음 작업을 수행합니다.  
  
    -   데이터 값을 저장할 S 매개 변수 버퍼의 배열을 할당합니다.  
  
    -   데이터 길이를 저장할 S개의 매개 변수 버퍼 배열을 할당합니다.  
  
    -   매개 변수 데이터 값과 데이터 길이 배열을 문 매개 변수에 바인딩할 SQLBindParameter를 호출 합니다.  
  
    -   매개 변수가 실행 시 데이터 text 또는 image 매개 변수인 경우 해당 매개 변수를 설정합니다.  
  
    -   실행 시 데이터 매개 변수를 사용하는 경우 해당 매개 변수를 설정합니다.  
  
6.  준비된 문을 실행할 때마다 다음 작업을 수행합니다.  
  
    -   S 데이터 값과 S 데이터 길이를 바인딩된 매개 변수 배열에 넣습니다.  
  
    -   준비 된 문을 실행 하는 SQLExecute를 호출 합니다.  
  
    -   실행 시 데이터 입력된 매개 변수를 사용 하면 SQLExecute SQL_NEED_DATA를 반환 합니다. SQLParamData 및 SQLPutData를 사용 하 여 데이터를 청크로 보냅니다.  
  
### <a name="to-prepare-a-statement-with-row-wise-bound-parameters"></a>행 단위 바인딩 매개 변수를 사용하여 문을 준비하려면  
  
1.  구조의 배열[S]을 할당합니다. 여기서 S는 매개 변수 집합의 수입니다. 구조에는 각 매개 변수에 대해 요소가 하나씩 포함되고 각 요소에는 두 부분이 포함됩니다.  
  
    -   첫 번째 부분은 매개 변수의 데이터를 보유하는 적절한 데이터 형식의 변수입니다.  
  
    -   두 번째 부분은 상태 표시를 보유하는 SQLINTEGER 변수입니다.  
  
2.  [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) 을 호출하여 다음 특성을 설정합니다.  
  
    -   SQL_ATTR_PARAMSET_SIZE를 매개 변수 집합 수(S)로 설정합니다.  
  
    -   SQL_ATTR_PARAM_BIND_TYPE을 1단계에서 할당한 구조의 크기로 설정합니다.  
  
    -   SQL_ATTR_PARAMS_PROCESSED_PTR 특성을 처리된 매개 변수 수를 보유하는 SQLUINTEGER 변수를 가리키도록 설정합니다.  
  
    -   SQL_ATTR_PARAMS_STATUS_PTR을 매개 변수 상태 표시를 보유하는 SQLUSSMALLINT 변수의 배열[S]을 가리키도록 설정합니다.  
  
3.  SQLPrepare에서 문 준비를 호출 합니다.  
  
4.  각 매개 변수 표식에 대 한 매개 변수 데이터 값과 데이터 길이 포인터가 1 단계에서에서 할당 한 구조 배열의 첫 번째 요소에 있는 해당 변수를 가리키도록 SQLBindParameter을 호출 합니다. 매개 변수가 실행 시 데이터 매개 변수인 경우 해당 매개 변수를 설정합니다.  
  
5.  준비된 문을 실행할 때마다 다음 작업을 수행합니다.  
  
    -   바인딩된 매개 변수 버퍼 배열을 데이터 값으로 채웁니다.  
  
    -   준비 된 문을 실행 하는 SQLExecute를 호출 합니다. 드라이버에서는 효율적으로 SQL 문을 각 매개 변수 집합에 대해 한 번씩 총 S번 실행합니다.  
  
    -   실행 시 데이터 입력된 매개 변수를 사용 하면 SQLExecute SQL_NEED_DATA를 반환 합니다. SQLParamData 및 SQLPutData를 사용 하 여 데이터를 청크로 보냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [방법 도움말 항목 쿼리를 실행할 &#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
---
title: "직접 문 실행 (ODBC) | Microsoft Docs"
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
helpviewer_keywords:
- statement execution
ms.assetid: b690f9de-66e1-4ee5-ab6a-121346fb5f85
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4471b9f4d85240a51d456ea90973c852f5e5db76
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="execute-a-statement-directly-odbc"></a>직접 문 실행(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-execute-a-statement-directly-and-one-time-only"></a>문을 한 번만 직접 실행하려면  
  
1.  문에 매개 변수 표식이 있으면 [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 를 사용하여 프로그램 변수에 각 매개 변수를 바인딩합니다. 프로그램 변수를 데이터 값으로 채운 다음 실행 시 데이터 매개 변수를 설정합니다.  
  
2.  [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) 를 호출하여 문을 실행합니다.  
  
3.  실행 시 데이터 입력 매개 변수를 사용하면 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) 는 SQL_NEED_DATA를 반환합니다. [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=58405) 및 [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)를 사용하여 데이터를 청크로 보냅니다.  
  
### <a name="to-execute-a-statement-multiple-times-by-using-column-wise-parameter-binding"></a>열 단위 매개 변수 바인딩을 사용하여 문을 여러 번 실행하려면  
  
1.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 을 호출하여 다음 특성을 설정합니다.  
  
     SQL_ATTR_PARAMSET_SIZE를 매개 변수 집합 수(S)로 설정합니다.  
  
     SQL_ATTR_PARAM_BIND_TYPE을 SQL_PARAMETER_BIND_BY_COLUMN으로 설정합니다.  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR 특성을 처리된 매개 변수 수를 보유하는 SQLUINTEGER 변수를 가리키도록 설정합니다.  
  
     SQL_ATTR_PARAMS_STATUS_PTR을 매개 변수 상태 표시를 보유하는 SQLUSSMALLINT 변수의 배열[S]을 가리키도록 설정합니다.  
  
2.  각 매개 변수 표식에 대해 다음 작업을 수행합니다.  
  
     데이터 값을 저장할 S 매개 변수 버퍼의 배열을 할당합니다.  
  
     데이터 길이를 저장할 S개의 매개 변수 버퍼 배열을 할당합니다.  
  
     [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 를 호출하여 매개 변수 데이터 값과 데이터 길이 배열을 문 매개 변수에 바인딩합니다.  
  
     실행 시 데이터 텍스트 또는 이미지 매개 변수를 설정합니다.  
  
     S개의 데이터 값과 S개의 데이터 길이를 바인딩된 매개 변수 배열에 넣습니다.  
  
3.  [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) 를 호출하여 문을 실행합니다. 드라이버에서는 효율적으로 문을 각 매개 변수 집합에 대해 한 번씩 총 S번 실행합니다.  
  
4.  실행 시 데이터 입력 매개 변수를 사용하면 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) 는 SQL_NEED_DATA를 반환합니다. [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=58405) 및 [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)를 사용하여 데이터를 청크로 보냅니다.  
  
### <a name="to-execute-a-statement-multiple-times-by-using-row-wise-parameter-binding"></a>행 단위 매개 변수 바인딩을 사용하여 문을 여러 번 실행하려면  
  
1.  구조의 배열[S]을 할당합니다. 여기서 S는 매개 변수 집합의 수입니다. 구조에는 각 매개 변수에 대해 요소가 하나씩 포함되고 각 요소에는 두 부분이 포함됩니다.  
  
     첫 번째 부분은 매개 변수의 데이터를 보유하는 적절한 데이터 형식의 변수입니다.  
  
     두 번째 부분은 상태 표시를 보유하는 SQLINTEGER 변수입니다.  
  
2.  [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 을 호출하여 다음 특성을 설정합니다.  
  
     SQL_ATTR_PARAMSET_SIZE를 매개 변수 집합 수(S)로 설정합니다.  
  
     SQL_ATTR_PARAM_BIND_TYPE을 1단계에서 할당한 구조의 크기로 설정합니다.  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR 특성을 처리된 매개 변수 수를 보유하는 SQLUINTEGER 변수를 가리키도록 설정합니다.  
  
     SQL_ATTR_PARAMS_STATUS_PTR을 매개 변수 상태 표시를 보유하는 SQLUSSMALLINT 변수의 배열[S]을 가리키도록 설정합니다.  
  
3.  각 매개 변수 표식에 대해 [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 를 호출하여 1단계에서 할당한 구조 배열의 첫 번째 요소에 있는 해당 변수에 대한 매개 변수 데이터 값 및 데이터 길이 포인터를 가리킵니다. 매개 변수가 실행 시 데이터 매개 변수인 경우 해당 매개 변수를 설정합니다.  
  
4.  바인딩된 매개 변수 버퍼 배열을 데이터 값으로 채웁니다.  
  
5.  [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) 를 호출하여 문을 실행합니다. 드라이버에서는 효율적으로 문을 각 매개 변수 집합에 대해 한 번씩 총 S번 실행합니다.  
  
6.  실행 시 데이터 입력 매개 변수를 사용하면 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) 는 SQL_NEED_DATA를 반환합니다. [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=58405) 및 [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md)를 사용하여 데이터를 청크로 보냅니다.  
  
 **참고** 열 단위 및 행 단위 바인딩은 일반적으로 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=59360) 보다는 [SQLPrepare 함수](http://go.microsoft.com/fwlink/?LinkId=58400) 및 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58399)와 함께 사용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [실행 중인 쿼리 방법 도움말 항목 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  

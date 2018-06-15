---
title: (ODBC) 결과 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41cca358deb729fda5d9659b9b76040cf8c3cc50
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32942278"
---
# <a name="processing-results---process-results"></a>처리 결과-결과 처리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

ODBC 응용 프로그램에서 결과 처리 먼저 결과 집합의 특징을 확인 한 다음 하나를 사용 하 여 프로그램 변수로 데이터를 검색 하려면 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) 또는 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)합니다.  
  
### <a name="to-process-results"></a>결과를 처리하려면  
  
1.  결과 집합 정보를 검색합니다.  
  
2.  바인딩된 열을 사용하는 경우 바인딩할 각 열에 대해 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)을 호출하여 프로그램 버퍼를 열에 바인딩합니다.  
  
3.  결과 집합의 각 행에 대해 다음을 수행합니다.  
  
    -   [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)를 호출하여 다음 행을 가져옵니다.  
  
    -   바인딩된 열을 사용하는 경우 이제 바인딩된 열 버퍼에서 사용할 수 있는 데이터를 사용합니다.  
  
    -   바인딩되지 않은 열을 사용하는 경우 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)를 한 번 이상 호출하여 바인딩된 마지막 열 다음의 바인딩되지 않은 열 데이터를 가져옵니다. **SQLGetData**는 번호가 가장 작은 열부터 차례로 호출해야 합니다.  
  
    -   **SQLGetData**를 여러 번 호출하여 텍스트나 이미지 열에서 데이터를 가져옵니다.  
  
4.  [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)에서 SQL_NO_DATA를 반환하여 결과 집합의 끝을 알리면 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 호출하여 다른 결과 집합을 사용할 수 있는지 여부를 확인합니다.  
  
    -   다른 결과 집합이 있으면 SQL_SUCCESS가 반환됩니다.  
  
    -   다른 결과 집합이 없으면 SQL_NO_DATA가 반환됩니다.  
  
    -   SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR가 반환되면 [SQLGetDiagRec](http://go.microsoft.com/fwlink/?LinkId=58402)를 호출하여 사용할 수 있는 PRINT 또는 RAISERROR 문 출력이 있는지 확인합니다.  
  
         바인딩된 문 매개 변수가 출력 매개 변수 또는 저장 프로시저의 반환 값으로 사용될 경우 바인딩된 매개 변수 버퍼에서 현재 사용할 수 있는 데이터를 사용합니다. 또한 바인딩된 매개 변수를 사용하면 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) 또는 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399)를 호출할 때마다 SQL 문이 *S*번 실행됩니다. 여기서 *S*는 바인딩된 매개 변수 배열에 포함된 요소 수입니다. 이는 *S*개의 결과 집합을 처리해야 함을 의미하며, 각 결과 집합은 SQL 문을 한 번 실행했을 때 일반적으로 반환되는 모든 결과 집합, 출력 매개 변수 및 반환 코드로 구성됩니다.  
  
    > [!NOTE]  
    >  결과 집합에 계산 행이 포함된 경우 각 계산 행은 별도의 결과 집합으로 사용할 수 있습니다. 이러한 계산 결과 집합은 일반 행 내에 섞여 일반 행을 여러 개의 결과 집합으로 나눕니다.  
  
5.  필요에 따라 SQL_UNBIND와 함께 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)를 호출하여 바인딩된 열 버퍼를 해제합니다.  
  
6.  다른 결과 집합을 사용할 수 있는 경우 1단계로 이동합니다.  
  
> [!NOTE]  
>  [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)에서 SQL_NO_DATA를 반환하기 전에 결과 집합 처리를 취소하려면 [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)를 호출합니다.  
  
## <a name="see-also"></a>관련 항목:  
[검색 결과 집합 정보 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-how-to/processing-results-retrieve-result-set-information.md)   
  
  

---
title: 결과 데이터 인출 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-results
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLFetchScroll function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], fetching
- SQLBindCol function
- result sets [ODBC], fetching
- fetching [ODBC]
- ODBC data types, fetching
- SQLFetch function
- SQL Server Native Client ODBC driver, data types
- SQLGetData function
ms.assetid: b289c7fb-5017-4d7e-a2d3-19401e9fc4cd
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8f1c828f3e63e3167a0685f450e318055a9b71fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="fetching-result-data"></a>결과 데이터 인출
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 응용 프로그램에는 결과 데이터를 인출하기 위한 세 가지 옵션이 있습니다.  
  
 첫 번째 옵션은 기반 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)합니다. 응용 프로그램에 사용 하 여 집합 결과 인출 하기 전에 **SQLBindCol** 각 열에 결과 집합을 프로그램 변수에 바인딩할 합니다. 변수에 현재 행의 데이터는 결과 집합 열에 바인딩된 각 드라이버 전송 응용 프로그램 호출 시간 열이 바인딩된 후 **SQLFetch** 또는 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)합니다. 결과 집합 열과 프로그램 변수의 데이터 형식이 다르면 드라이버가 데이터 변환을 처리합니다. 응용 프로그램에서 1 보다 큰 설정 SQL_ATTR_ROW_ARRAY_SIZE를 바인딩할 수 있는 결과 열 모두 채워짐을 호출할 때마다 변수의 배열 **SQLFetchScroll**합니다.  
  
 두 번째 옵션은 기반 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)합니다. 응용 프로그램을 사용 하지 않는 **SQLBindCol** 결과 바인딩할 열을 프로그램 변수에 설정 합니다. 호출할 때마다 **SQLFetch**, 응용 프로그램 호출 **SQLGetData** 되 면 결과의 각 열에 대 한 설정입니다. **SQLGetData** 드라이버가 특정 결과 집합 열에서 특정 프로그램 변수로 데이터를 전송 하도록 지시 하 고 열과 변수의 데이터 형식을 지정 합니다. 이를 통해 드라이버는 결과 열과 프로그램 변수의 데이터 형식이 다를 경우 데이터를 변환할 수 있습니다. **텍스트**, **ntext**, 및 **이미지** 열은 대개 너무 커서 프로그램 변수에 맞지 않지만 계속 사용 하 여 검색할 수 **SQLGetData**합니다. 경우는 **텍스트**, **ntext**, 또는 **이미지** 결과 열에 데이터를 프로그램 변수에 초과 **SQLGetData** SQL_SUCCESS_ 반환 WITH_INFO 및 SQLSTATE 01004 (문자열 데이터, 오른쪽이 잘렸습니다). 에 대 한 연속 호출은 **SQLGetData** 의 청크가 반환 된 **텍스트** 또는 **이미지** 데이터입니다. 데이터의 끝에 도달 하면 **SQLGetData** 관계 없이 SQL_SUCCESS를 반환 합니다. SQL_ATTR_ROW_ARRAY_SIZE가 1보다 크면 각 인출에서 일련의 행 또는 행 집합을 반환합니다. 사용 하기 전에 **SQLGetData**, 먼저 사용 해야 **SQLSetPos** 현재 행으로 행 집합 내의 특정 행을 지정할 수 있습니다.  
  
 함께 사용 하 여 세 번째 옵션은 **SQLBindCol** 및 **SQLGetData**합니다. 응용 프로그램 수 예를 들어 결과 집합의 처음 10 개 열을 바인딩할 하 고, 그런 다음 각 인출에서 호출 **SQLGetData** 세 번 세 바인딩되지 않은 열에서 데이터를 검색 합니다. 이 일반적으로 사용할 하나 이상의 결과 집합에 포함 되어 있으면 **텍스트** 또는 **이미지** 열입니다.  
  
 응용 프로그램은 결과 집합에 대해 설정 된 커서 옵션에 따라의 스크롤 옵션을 사용할 수도 수 **SQLFetchScroll** 스크롤 하는 결과 집합입니다.  
  
 과도 하 게 사용 **SQLBindCol** 바인딩하는 결과 집합 열을 프로그램 변수에 듭니다 때문에 **SQLBindCol** ODBC 드라이버가 메모리를 할당 합니다. 변수에 결과 열을 바인딩하는 경우 해당 바인딩을 때까지 유효 하거나 호출 [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 가능한 문 핸들 또는 호출으로 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 와 *fOption* QL_UNBIND로 설정 합니다. 바인딩은 문이 완료될 때 자동으로 취소되지 않습니다.  
  
 이 논리를 이용해 서로 다른 매개 변수를 사용하는 동일 SELECT 문의 복수 실행을 효과적으로 처리할 수 있습니다. 결과 집합을 한 번 바인딩할 모든 SELECT 문의 처리 수 있으므로 동일한 구조를 유지 하는 결과 집합을 다음 호출 **SQLFreeStmt** 와 *fOption* 마지막으로 실행 한 후 QL_UNBIND로 설정 합니다. 호출 하지 않아야 **SQLBindCol** 결과 먼저 호출 하지 않고 집합의 열을 바인딩하 **SQLFreeStmt** 와 *fOption* 이전 바인딩을을 SQL_UNBIND로 설정 합니다.  
  
 사용 하는 경우 **SQLBindCol**를 행 단위로 또는 열 단위 바인딩 안 함 중 하나를 수행할 수 있습니다. 행 단위 바인딩은 열 단위 바인딩보다 빠릅니다.  
  
 사용할 수 있습니다 **SQLGetData** 바인딩 결과 아닌 열 단위로 단위로 데이터를 검색 하려면 사용 하 여 열을 설정 **SQLBindCol**합니다. 사용 하 여 결과 집합 행을 몇 개만 있으면 **SQLGetData** 대신 **SQLBindCol** 그렇지 않으면 빠른 **SQLBindCol** 최상의 성능을 제공 합니다. 동일한 변수 집합에 데이터를 항상 배치 하지 않는 경우에 사용 해야 **SQLGetData** 계속 해 서 다시 바인딩하는 대신 합니다. 만 사용할 수 있습니다 **SQLGetData** 모든 열을 바인딩한 후 select 목록에는 열에 **SQLBindCol**합니다. 열에 이미 사용 하는 모든 열 뒤 나타나야 **SQLGetData**합니다.  
  
 데이터를 내부 또는 프로그램 변수에서와 같은 이동를 처리 하는 ODBC 함수 **SQLGetData**, **SQLBindCol**, 및 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), 암시적 데이터 형식 지원 변환 합니다. 예를 들어 응용 프로그램이 정수 열을 문자열 프로그램 변수에 바인딩할 경우 드라이버는 해당 데이터를 자동으로 정수에서 문자로 변환한 후 이를 프로그램 변수에 전달합니다.  
  
 응용 프로그램에서의 데이터 변환은 최소화해야 합니다. 응용 프로그램에서 수행하는 처리에 데이터 변환이 반드시 필요한 경우가 아니면 응용 프로그램은 열과 매개 변수를 동일한 형식의 프로그램 변수에 바인딩해야 합니다. 데이터 형식 변환이 반드시 필요한 경우에는 응용 프로그램에서가 아니라 드라이버가 변환을 수행하도록 하는 것이 효율적입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 일반적으로 네트워크 버퍼에서 응용 프로그램의 변수에 직접 데이터를 전달합니다. 데이터 변환을 수행하도록 드라이버에 요청하면 드라이버는 데이터를 버퍼링한 후 CPU 주기를 사용하여 데이터를 변환합니다.  
  
 프로그램 변수에서 전달 된 열을 제외 하 고 데이터를 보관 하기에 충분 해야 **텍스트**, **ntext**, 및 **이미지** 데이터입니다. 응용 프로그램이 결과 집합 데이터를 검색한 후 해당 데이터를 수용하기에 너무 작은 변수에 데이터를 삽입하려고 하면 드라이버가 경고를 생성합니다. 이 경우 드라이버는 메시지에 사용할 메모리를 할당하게 되고 드라이버와 응용 프로그램 모두 메시지 및 오류 처리를 위해 CPU 주기를 사용해야 합니다. 응용 프로그램은 검색된 데이터를 수용할 수 있을 만큼 큰 변수를 할당하거나 SELECT 목록에서 SUBSTRING 함수를 사용하여 결과 집합의 열 크기를 줄여야 합니다.  
  
 SQL_C_DEFAULT를 사용하여 C 변수의 형식을 지정할 때는 주의를 기울여야 합니다. SQL_C_DEFAULT는 C 변수 형식이 열이나 매개 변수의 SQL 데이터 형식과 일치하도록 지정합니다. 에 대해 SQL_C_DEFAULT를 지정 하는 경우는 **ntext**, **nchar**, 또는 **nvarchar** 열에서 비유니코드 데이터는 응용 프로그램에 반환 됩니다. 유니코드 데이터를 처리하도록 응용 프로그램이 코딩되지 않은 경우 이로 인해 여러 가지 문제가 발생할 수 있습니다. 같은 종류의 문제가 발생할 수 있습니다는 **uniqueidentifier** (SQL_GUID) 데이터 형식입니다.  
  
 **텍스트**, **ntext**, 및 **이미지** 데이터는 일반적으로 너무 커서 단일 프로그램 변수에 맞지와 함께 처리 하 여 일반적으로 **SQLGetData** 대신 **SQLBindCol**합니다. 서버 커서를 사용 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 바인딩되지 않은 대 한 데이터를 전송 하지 않도록 최적화 되어 **텍스트**, **ntext**, 또는 **이미지** 열에는 행 인출 되는 시간입니다. **텍스트**, **ntext**, 또는 **이미지** 데이터 실제로에서 검색 되지 않는 서버 응용 프로그램 문제까지 **SQLGetData** 열에 대 한 합니다.  
  
 이 최적화를 응용 프로그램에 적용할 수 있도록 없는 **텍스트**, **ntext**, 또는 **이미지** 데이터는 사용자가 커서를 위나 아래로 스크롤 하는 동안 표시 됩니다. 응용 프로그램을 호출할 수 있는 행을 선택한 후 **SQLGetData** 검색 하는 **텍스트**, **ntext**, 또는 **이미지** 데이터입니다. 이렇게 하면 전송에서 **텍스트**, **ntext**, 또는 **이미지** 데이터 행에 대 한 사용자 선택 하지 못하는 및 전송 매우 많은 양의 데이터를 저장할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [결과 처리 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  

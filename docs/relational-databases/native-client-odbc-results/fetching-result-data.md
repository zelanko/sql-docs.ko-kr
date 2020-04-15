---
title: 결과 데이터 가져오기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1d9fdfcd7bcc4f86afacc75dff5b40b77bb7b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304619"
---
# <a name="fetching-result-data"></a>결과 데이터 인출
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 애플리케이션에는 결과 데이터를 인출하기 위한 세 가지 옵션이 있습니다.  
  
 첫 번째 옵션은 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)을 기반으로 합니다. 결과 집합을 가져오기 전에 응용 프로그램은 **SQLBindCol을** 사용하여 결과 집합의 각 열을 프로그램 변수에 바인딩합니다. 열이 바인딩된 후 드라이버는 응용 프로그램에서 **SQLFetch** 또는 [SQLFetchScroll를](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)호출할 때마다 현재 행의 데이터를 결과 집합 열에 바인딩된 변수로 전송합니다. 결과 집합 열과 프로그램 변수의 데이터 형식이 다르면 드라이버가 데이터 변환을 처리합니다. 응용 프로그램이 SQL_ATTR_ROW_ARRAY_SIZE 1보다 큰 설정이 있는 경우 결과 열을 변수 배열에 바인딩할 수 있으며, 이 열은 **SQLFetchScroll**에 대한 각 호출마다 채워집니다.  
  
 두 번째 옵션은 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). 응용 프로그램은 **SQLBindCol을** 사용하여 결과 집합 열을 프로그램 변수에 바인딩하지 않습니다. **SQLFetch를**호출할 때마다 응용 프로그램은 결과 집합의 각 열에 대해 **SQLGetData를** 한 번 호출합니다. **SQLGetData는** 드라이버에게 특정 결과 집합 열에서 특정 프로그램 변수로 데이터를 전송하도록 지시하고 열 및 변수의 데이터 형식을 지정합니다. 이를 통해 드라이버는 결과 열과 프로그램 변수의 데이터 형식이 다를 경우 데이터를 변환할 수 있습니다. **텍스트,** **ntext**및 **이미지** 열은 일반적으로 프로그램 변수에 맞지 않을 정도로 크지만 **SQLGetData**를 사용하여 검색할 수 있습니다. 결과 열의 **텍스트,** **ntext**또는 **이미지** 데이터가 프로그램 변수보다 큰 경우 **SQLGetData는** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004(문자열 데이터, 오른쪽 잘린)를 반환합니다. **SQLGetData에** 대한 연속 호출은 **텍스트** 또는 **이미지** 데이터의 연속된 청크를 반환합니다. 데이터의 끝에 도달하면 **SQLGetData는** SQL_SUCCESS 반환합니다. SQL_ATTR_ROW_ARRAY_SIZE가 1보다 크면 각 인출에서 일련의 행 또는 행 집합을 반환합니다. **SQLGetData를**사용하기 전에 먼저 **SQLSetPos를** 사용하여 행 집합 내의 특정 행을 현재 행으로 지정해야 합니다.  
  
 세 번째 옵션은 **SQLBindCol** 및 **SQLGetData를**혼합하여 사용하는 것입니다. 예를 들어 응용 프로그램은 결과 집합의 처음 10개의 열을 바인딩한 다음 각 가져오기에서 **SQLGetData를** 세 번 호출하여 세 개의 언바운드 열에서 데이터를 검색할 수 있습니다. 일반적으로 결과 집합에 하나 이상의 **텍스트** 또는 **이미지** 열이 포함된 경우에 사용됩니다.  
  
 결과 집합에 대해 설정된 커서 옵션에 따라 응용 프로그램에서 **SQLFetchScroll의** 스크롤 옵션을 사용하여 결과 집합 을 스크롤할 수도 있습니다.  
  
 **SQLBindCol은 ODBC** 드라이버가 메모리를 할당하는 원인이 되기 때문에 결과 집합 열을 프로그램 변수에 바인딩하기 위해 **SQLBindCol을** 과도하게 사용하면 비용이 많이 듭니다. 결과 열을 변수에 바인딩하면 [SQLFreeHandle을](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 호출하여 문 핸들을 해제하거나 *fOption을* SQL_UNBIND 설정하여 [SQLFreeStmt를](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 호출할 때까지 해당 바인딩이 계속 적용됩니다. 바인딩은 문이 완료될 때 자동으로 취소되지 않습니다.  
  
 이 논리를 이용해 서로 다른 매개 변수를 사용하는 동일 SELECT 문의 복수 실행을 효과적으로 처리할 수 있습니다. 결과 집합은 동일한 구조를 유지하므로 결과 집합을 한 번 바인딩하고 모든 SELECT 문을 처리한 다음 마지막 실행 후 *SQL_UNBIND fOption을* 사용하여 **SQLFreeStmt를** 호출할 수 있습니다. **SQLBindCol을** 호출하여 이전 바인딩을 해제하도록 SQL_UNBIND *fOption* 을 사용하여 **먼저 SQLFreeStmt를** 호출하지 않고 결과 집합에서 열을 바인딩할 수 없습니다.  
  
 **SQLBindCol을**사용하는 경우 행 별 또는 열 별 바인딩을 수행 할 수 있습니다. 행 단위 바인딩은 열 단위 바인딩보다 빠릅니다.  
  
 **SQLGetData를** 사용하여 **SQLBindCol**을 사용하여 결과 집합 열을 바인딩하는 대신 열단위로 데이터를 검색할 수 있습니다. 결과 집합에 몇 개의 행만 포함되는 경우 **SQLBindCol** 대신 **SQLGetData를** 사용하는 것이 더 빠릅니다. 그렇지 않으면 **SQLBindCol이** 최상의 성능을 제공합니다. 항상 동일한 변수 집합에 데이터를 넣지 않는 경우 지속적으로 바인딩하는 대신 **SQLGetData를** 사용해야 합니다. 모든 열이 **SQLBindCol**로 바인딩된 후에선택 목록에 있는 열에만 **SQLGetData를** 사용할 수 있습니다. 열은 **SQLGetData**를 이미 사용한 열 후에도 나타나야 합니다.  
  
 **SQLGetData,** **SQLBindCol**및 [SQLBindParameter와](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)같은 프로그램 변수로 또는 외부로 데이터를 이동하는 것을 처리하는 ODBC 함수는 암시적 데이터 형식 변환을 지원합니다. 예를 들어 애플리케이션이 정수 열을 문자열 프로그램 변수에 바인딩할 경우 드라이버는 해당 데이터를 자동으로 정수에서 문자로 변환한 후 이를 프로그램 변수에 전달합니다.  
  
 애플리케이션에서의 데이터 변환은 최소화해야 합니다. 애플리케이션에서 수행하는 처리에 데이터 변환이 반드시 필요한 경우가 아니면 애플리케이션은 열과 매개 변수를 동일한 형식의 프로그램 변수에 바인딩해야 합니다. 데이터 형식 변환이 반드시 필요한 경우에는 애플리케이션에서가 아니라 드라이버가 변환을 수행하도록 하는 것이 효율적입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 일반적으로 네트워크 버퍼에서 애플리케이션의 변수에 직접 데이터를 전달합니다. 데이터 변환을 수행하도록 드라이버에 요청하면 드라이버는 데이터를 버퍼링한 후 CPU 주기를 사용하여 데이터를 변환합니다.  
  
 프로그램 변수는 **텍스트,** **ntext**및 **이미지** 데이터를 제외하고 열에서 전송되는 데이터를 보유할 수 있을 만큼 커야 합니다. 애플리케이션이 결과 집합 데이터를 검색한 후 해당 데이터를 수용하기에 너무 작은 변수에 데이터를 삽입하려고 하면 드라이버가 경고를 생성합니다. 이 경우 드라이버는 메시지에 사용할 메모리를 할당하게 되고 드라이버와 애플리케이션 모두 메시지 및 오류 처리를 위해 CPU 주기를 사용해야 합니다. 애플리케이션은 검색된 데이터를 수용할 수 있을 만큼 큰 변수를 할당하거나 SELECT 목록에서 SUBSTRING 함수를 사용하여 결과 집합의 열 크기를 줄여야 합니다.  
  
 SQL_C_DEFAULT를 사용하여 C 변수의 형식을 지정할 때는 주의를 기울여야 합니다. SQL_C_DEFAULT는 C 변수 형식이 열이나 매개 변수의 SQL 데이터 형식과 일치하도록 지정합니다. **ntext,** **nchar**또는 **nvarchar** 열에 대해 SQL_C_DEFAULT 지정하면 유니코드 데이터가 응용 프로그램에 반환됩니다. 유니코드 데이터를 처리하도록 애플리케이션이 코딩되지 않은 경우 이로 인해 여러 가지 문제가 발생할 수 있습니다. **고유 식별자(SQL_GUID)** 데이터 형식과 동일한 유형의 문제가 발생할 수 있습니다.  
  
 **텍스트**, **ntext**및 **이미지** 데이터는 일반적으로 단일 프로그램 변수에 맞지 너무 크며 일반적으로 **SQLBindCol**대신 **SQLGetData로** 처리됩니다. 서버 커서를 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 행을 가져올 때 언바운드 **텍스트,** **ntext**또는 **이미지** 열에 대한 데이터를 전송하지 않도록 최적화됩니다. 응용 프로그램이 열에 **대해 SQLGetData를** 발행할 때까지 **텍스트,** **ntext**또는 **이미지** 데이터는 서버에서 실제로 검색되지 않습니다.  
  
 이 최적화는 사용자가 커서를 위아래로 스크롤하는 동안 **텍스트,** **ntext**또는 **이미지** 데이터가 표시되지 않도록 응용 프로그램에 적용할 수 있습니다. 사용자가 행을 선택한 후 응용 프로그램은 **SQLGetData를** 호출하여 **텍스트,** **ntext**또는 **이미지** 데이터를 검색할 수 있습니다. 이렇게 하면 사용자가 선택하지 않는 행에 대한 **텍스트,** **ntext**또는 **이미지** 데이터를 전송하고 매우 많은 양의 데이터를 전송할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;처리 결과](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  

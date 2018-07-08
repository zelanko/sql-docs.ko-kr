---
title: 결과 데이터 인출 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-results
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2a6544740b8f1ba2c24b60bfadcf26492204e429
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413094"
---
# <a name="fetching-result-data"></a>결과 데이터 인출
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 응용 프로그램에는 결과 데이터를 인출하기 위한 세 가지 옵션이 있습니다.  
  
 첫 번째 옵션은 기반 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)합니다. 응용 프로그램에서는 설정 결과 인출 하기 전에 **SQLBindCol** 각 열에 결과 집합을 프로그램 변수에 바인딩할 합니다. 변수에 현재 행의 데이터는 결과 집합 열에 바인딩된 각 드라이버 전송 응용 프로그램이 호출 시간 열이 바인딩된 후 **SQLFetch** 하거나 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)합니다. 결과 집합 열과 프로그램 변수의 데이터 형식이 다르면 드라이버가 데이터 변환을 처리합니다. 응용 프로그램에는 1 보다 크게 설정 하는 SQL_ATTR_ROW_ARRAY_SIZE를 바인딩할 수 있는 결과 열 모두 채워집니다를 호출할 때마다 변수의 배열 **SQLFetchScroll**합니다.  
  
 두 번째 옵션은 기반 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)합니다. 응용 프로그램을 사용 하지 않습니다 **SQLBindCol** 결과 바인딩할 열을 프로그램 변수에 설정 합니다. 호출한 후 **SQLFetch**, 응용 프로그램이 호출 **SQLGetData** 결과의 각 열에 대해 설정 합니다. **SQLGetData** 열과 변수의 데이터 형식을 지정 하 고 드라이버 특정 프로그램 변수에 특정 결과 집합 열에서 데이터를 전송에 지시 합니다. 이를 통해 드라이버는 결과 열과 프로그램 변수의 데이터 형식이 다를 경우 데이터를 변환할 수 있습니다. **텍스트**하십시오 **ntext**, 및 **이미지** 열은 대개 너무 커서 프로그램 변수에 맞지 않지만 여전히 사용 하 여 검색할 수 있습니다 **SQLGetData**합니다. 경우는 **텍스트**를 **ntext**, 또는 **이미지** 결과 열에 데이터가 프로그램 변수 보다 큰 **SQLGetData** SQL_SUCCESS_를 반환 합니다. WITH_INFO 및 SQLSTATE 01004 (문자열 데이터, 오른쪽이 잘렸습니다). 에 대 한 연속 호출 **SQLGetData** 의 청크가 반환 된 **텍스트** 또는 **이미지** 데이터입니다. 데이터의 끝에 도달 하면 **SQLGetData** 관계 없이 SQL_SUCCESS를 반환 합니다. SQL_ATTR_ROW_ARRAY_SIZE가 1보다 크면 각 인출에서 일련의 행 또는 행 집합을 반환합니다. 사용 하기 전에 **SQLGetData**를 먼저 사용 해야 **SQLSetPos** 현재 행으로 행 집합 내의 특정 행을 지정 합니다.  
  
 세 번째 옵션은 함께 사용할 **SQLBindCol** 하 고 **SQLGetData**합니다. 응용 프로그램 수, 예를 들어 결과 집합의 처음 10 개의 열을 바인딩하려면 및 그런 다음 각 인출 시 호출할 **SQLGetData** 세 번 세 바인딩되지 않은 열에서 데이터를 검색 합니다. 이 일반적으로 사용할 하나 이상의 결과 집합에 포함 되어 있으면 **텍스트** 하거나 **이미지** 열입니다.  
  
 응용 프로그램은 결과 집합에 대해 설정 된 커서 옵션에 따라의 스크롤 옵션을 사용할 수도 있습니다 **SQLFetchScroll** 결과 집합 내 스크롤해야 합니다.  
  
 과도 하 게 사용 **SQLBindCol** 바인딩하는 결과 집합 열을 프로그램 변수에 듭니다 있으므로 **SQLBindCol** ODBC 드라이버가 메모리를 할당 합니다. 결과 열을 변수에 바인딩할 때 바인딩이 유효 하거나 호출 [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 호출을 문 핸들을 해제 하려면 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 사용 하 여 *fOption* SQL_UNBIND로 설정 합니다. 바인딩은 문이 완료될 때 자동으로 취소되지 않습니다.  
  
 이 논리를 이용해 서로 다른 매개 변수를 사용하는 동일 SELECT 문의 복수 실행을 효과적으로 처리할 수 있습니다. 결과 집합을 한 번 바인딩할 모든 SELECT 문의 처리 수 있으므로 동일한 구조를 유지 하는 결과 집합을 호출 **SQLFreeStmt** 사용 하 여 *fOption* 마지막 실행 한 후 SQL_UNBIND로 설정 합니다. 호출 하지 않아야 **SQLBindCol** 결과 첫 번째 호출 하지 않고 집합에 열을 바인딩하려면 **SQLFreeStmt** 사용 하 여 *fOption* 이전 바인딩을을 SQL_UNBIND로 설정 합니다.  
  
 사용 하는 경우 **SQLBindCol**, 행 단위 또는 열 단위 바인딩 중 하나 수행 할 수 있습니다. 행 단위 바인딩은 열 단위 바인딩보다 빠릅니다.  
  
 사용할 수 있습니다 **SQLGetData** 사용 하 여 열 집합 결과 바인딩하는 대신 하 여 열 단위로 데이터를 검색할 **SQLBindCol**합니다. 사용 하 여 결과 집합 행을 몇 개만 들어 있으면 **SQLGetData** of **SQLBindCol** 고, 그렇지 않으면 빠른 **SQLBindCol** 최상의 성능을 제공 합니다. 변수의 동일한 집합에 데이터를 항상 저장 하지 않는 경우 사용 해야 **SQLGetData** 지속적으로 다시 바인딩하는 대신 합니다. 만 사용할 수 있습니다 **SQLGetData** 사용 하 여 모든 열을 바인딩한 후 select 목록에 있는 열에 **SQLBindCol**합니다. 이미 사용 하는 모든 열 뒤에 열 표시도 되어야 **SQLGetData**합니다.  
  
 ODBC 함수는 데이터를 프로그램 변수에 안팎으로 같은 이동 다루는 **SQLGetData**를 **SQLBindCol**, 및 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), 암시적 데이터 형식 지원 변환 합니다. 예를 들어 응용 프로그램이 정수 열을 문자열 프로그램 변수에 바인딩할 경우 드라이버는 해당 데이터를 자동으로 정수에서 문자로 변환한 후 이를 프로그램 변수에 전달합니다.  
  
 응용 프로그램에서의 데이터 변환은 최소화해야 합니다. 응용 프로그램에서 수행하는 처리에 데이터 변환이 반드시 필요한 경우가 아니면 응용 프로그램은 열과 매개 변수를 동일한 형식의 프로그램 변수에 바인딩해야 합니다. 데이터 형식 변환이 반드시 필요한 경우에는 응용 프로그램에서가 아니라 드라이버가 변환을 수행하도록 하는 것이 효율적입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 일반적으로 네트워크 버퍼에서 응용 프로그램의 변수에 직접 데이터를 전달합니다. 데이터 변환을 수행하도록 드라이버에 요청하면 드라이버는 데이터를 버퍼링한 후 CPU 주기를 사용하여 데이터를 변환합니다.  
  
 프로그램 변수에서 전달 된 열을 제외 하 고 데이터를 저장 하기에 충분 해야 **텍스트**를 **ntext**, 및 **이미지** 데이터입니다. 응용 프로그램이 결과 집합 데이터를 검색한 후 해당 데이터를 수용하기에 너무 작은 변수에 데이터를 삽입하려고 하면 드라이버가 경고를 생성합니다. 이 경우 드라이버는 메시지에 사용할 메모리를 할당하게 되고 드라이버와 응용 프로그램 모두 메시지 및 오류 처리를 위해 CPU 주기를 사용해야 합니다. 응용 프로그램은 검색된 데이터를 수용할 수 있을 만큼 큰 변수를 할당하거나 SELECT 목록에서 SUBSTRING 함수를 사용하여 결과 집합의 열 크기를 줄여야 합니다.  
  
 SQL_C_DEFAULT를 사용하여 C 변수의 형식을 지정할 때는 주의를 기울여야 합니다. SQL_C_DEFAULT는 C 변수 형식이 열이나 매개 변수의 SQL 데이터 형식과 일치하도록 지정합니다. 대해 SQL_C_DEFAULT를 지정 하는 경우는 **ntext**를 **nchar**, 또는 **nvarchar** 열에서 비유니코드 데이터는 응용 프로그램에 반환 됩니다. 유니코드 데이터를 처리하도록 응용 프로그램이 코딩되지 않은 경우 이로 인해 여러 가지 문제가 발생할 수 있습니다. 같은 종류의 문제가 발생할 수 있습니다 합니다 **uniqueidentifier** (SQL_GUID) 데이터 형식입니다.  
  
 **텍스트**하십시오 **ntext**, 및 **이미지** 데이터는 일반적으로 너무 커서 단일 프로그램 변수에 맞지 및 일반적으로 처리 됩니다 **SQLGetData** 대신 **SQLBindCol**합니다. 서버 커서를 사용 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 바인딩되지 않은 대 한 데이터를 전송 하지 않도록 최적화 되어 **텍스트**를 **ntext**, 또는 **이미지** 열에는 행 인출 되는 시간입니다. **텍스트**, **ntext**, 또는 **이미지** 데이터는 검색 되지 않습니다 서버에서 응용 프로그램 문제까지 **SQLGetData** 에 열입니다.  
  
 이 최적화를 응용 프로그램에 적용할 수 있도록 없습니다 **텍스트**를 **ntext**, 또는 **이미지** 사용자 커서를 위나 아래로 스크롤 하는 동안 데이터가 표시 됩니다. 사용자가 행을 선택 후 응용 프로그램을 호출 하 수 **SQLGetData** 검색 하는 **텍스트**를 **ntext**, 또는 **이미지** 데이터입니다. 전송할 저장 합니다 **텍스트**, **ntext**, 또는 **이미지** 데이터 행에 대 한 사용자 선택 되지 않습니다 및 전송 매우 많은 양의 데이터를 저장할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [결과 처리 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  

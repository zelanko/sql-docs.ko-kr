---
title: 결과 데이터를 페치하는 중 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5d4dc78d946f76161cbe7210e183d9b3b77be955
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82699290"
---
# <a name="fetching-result-data"></a>결과 데이터 인출
  ODBC 애플리케이션에는 결과 데이터를 인출하기 위한 세 가지 옵션이 있습니다.  
  
 첫 번째 옵션은 [SQLBindCol](../native-client-odbc-api/sqlbindcol.md)를 기반으로 합니다. 응용 프로그램은 결과 집합을 가져오기 전에 **SQLBindCol** 를 사용 하 여 결과 집합의 각 열을 프로그램 변수에 바인딩합니다. 열이 바인딩된 후 드라이버는 응용 프로그램이 **Sqlfetch** 또는 [sqlfetchscroll](../native-client-odbc-api/sqlfetchscroll.md)을 호출할 때마다 현재 행의 데이터를 결과 집합 열에 바인딩된 변수로 전송 합니다. 결과 집합 열과 프로그램 변수의 데이터 형식이 다르면 드라이버가 데이터 변환을 처리합니다. 응용 프로그램 SQL_ATTR_ROW_ARRAY_SIZE 1 보다 크게 설정 된 경우 결과 열을 변수 배열에 바인딩할 수 있습니다 .이는 모두 **Sqlfetchscroll**에 대 한 각 호출에 채워집니다.  
  
 두 번째 옵션은 [SQLGetData](../native-client-odbc-api/sqlgetdata.md)를 기반으로 합니다. 응용 프로그램은 **SQLBindCol** 를 사용 하 여 결과 집합 열을 프로그램 변수에 바인딩합니다. **Sqlfetch**를 호출할 때마다 응용 프로그램은 결과 집합의 각 열에 대해 한 번씩 **SQLGetData** 를 호출 합니다. **SQLGetData** 는 특정 결과 집합 열에서 특정 프로그램 변수로 데이터를 전송 하도록 드라이버에 지시 하 고 열과 변수의 데이터 형식을 지정 합니다. 이를 통해 드라이버는 결과 열과 프로그램 변수의 데이터 형식이 다를 경우 데이터를 변환할 수 있습니다. **Text**, **ntext**및 **image** 열은 일반적으로 너무 커서 프로그램 변수에 맞지 않지만 **SQLGetData**를 사용 하 여 검색할 수 있습니다. 결과 열에 있는 **text**, **ntext**또는 **image** 데이터가 프로그램 변수 보다 큰 경우 **SQLGetData** 는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (문자열 데이터, 오른쪽 잘림)을 반환 합니다. **SQLGetData** 에 대 한 연속 호출은 **텍스트** 또는 **이미지** 데이터의 연속 청크를 반환 합니다. 데이터의 끝에 도달 하면 **SQLGetData** 는 SQL_SUCCESS을 반환 합니다. SQL_ATTR_ROW_ARRAY_SIZE가 1보다 크면 각 인출에서 일련의 행 또는 행 집합을 반환합니다. **SQLGetData**를 사용 하기 전에 먼저 **SQLSetPos** 를 사용 하 여 행 집합 내의 특정 행을 현재 행으로 지정 해야 합니다.  
  
 세 번째 옵션은 혼합 **SQLBindCol** 및 **SQLGetData**를 사용 하는 것입니다. 예를 들어 응용 프로그램은 결과 집합의 처음 10 개 열을 바인딩한 다음 반입할 때마다 **SQLGetData** 를 세 번 호출 하 여 세 개의 바인딩되지 않은 열에서 데이터를 검색 합니다. 일반적으로 결과 집합에 하나 이상의 **텍스트** 또는 **이미지** 열이 포함 된 경우에 사용 됩니다.  
  
 결과 집합에 대해 설정 된 커서 옵션에 따라 응용 프로그램은 **Sqlfetchscroll** 의 스크롤 옵션을 사용 하 여 결과 집합을 스크롤할 수도 있습니다.  
  
 **SQLBindCol** 에서 ODBC 드라이버가 메모리를 할당 하기 때문에 **SQLBindCol** 를 과도 하 게 사용 하면 결과 집합 열을 프로그램 변수에 바인딩할 수 있습니다. 결과 열을 변수에 바인딩하는 경우 [Sqlfreehandle](../native-client-odbc-api/sqlfreehandle.md) 을 호출 하 여 문 핸들을 해제 하거나 *foption* 이 SQL_UNBIND로 설정 된 [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) 를 호출할 때까지 해당 바인딩은 적용 된 상태로 유지 됩니다. 바인딩은 문이 완료될 때 자동으로 취소되지 않습니다.  
  
 이 논리를 이용해 서로 다른 매개 변수를 사용하는 동일 SELECT 문의 복수 실행을 효과적으로 처리할 수 있습니다. 결과 집합이 동일한 구조를 유지 하기 때문에 결과 집합을 한 번 바인딩하고, 모든 SELECT 문을 처리 한 다음, 마지막 실행 후 SQL_UNBIND으로 *Foption* 을 설정 하 여 **SQLFreeStmt** 를 호출할 수 있습니다. **SQLBindCol** SQL_UNBIND를 호출 하 여 SQLFreeStmt로 설정 된 *Foption* 이 있는 **SQLFreeStmt** 를 먼저 호출 하지 않고 결과 집합의 열을 바인딩하려면 먼저 이전 바인딩을 해제 해야 합니다.  
  
 **SQLBindCol**를 사용 하는 경우 행 단위 또는 열 단위 바인딩을 수행할 수 있습니다. 행 단위 바인딩은 열 단위 바인딩보다 빠릅니다.  
  
 **SQLBindCol**를 사용 하 여 결과 집합 열을 바인딩하지 않고 열 단위로 데이터를 검색 하는 데 **SQLGetData** 를 사용할 수 있습니다. 결과 집합에 몇 개의 행만 포함 되어 있는 경우 **SQLBindCol** 대신 **SQLGetData** 를 사용 하는 것이 더 빠릅니다. 그렇지 않으면 **SQLBindCol** 는 최상의 성능을 제공 합니다. 항상 동일한 변수 집합에 데이터를 저장 하지 않는 경우에는 지속적으로 리바인딩 대신 **SQLGetData** 를 사용 해야 합니다. **SQLBindCol**를 사용 하 여 모든 열이 바인딩된 후에는 선택 목록에 있는 열에 대해서만 **SQLGetData** 를 사용할 수 있습니다. 이 열은 이미 **SQLGetData**를 사용한 열 뒤에도 나타나야 합니다.  
  
 **SQLGetData**, **SQLBindCol**및 [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)와 같이 프로그램 변수로 데이터를 이동 하거나 외부로 이동 하는 것을 처리 하는 ODBC 함수는 암시적 데이터 형식 변환을 지원 합니다. 예를 들어 애플리케이션이 정수 열을 문자열 프로그램 변수에 바인딩할 경우 드라이버는 해당 데이터를 자동으로 정수에서 문자로 변환한 후 이를 프로그램 변수에 전달합니다.  
  
 애플리케이션에서의 데이터 변환은 최소화해야 합니다. 애플리케이션에서 수행하는 처리에 데이터 변환이 반드시 필요한 경우가 아니면 애플리케이션은 열과 매개 변수를 동일한 형식의 프로그램 변수에 바인딩해야 합니다. 데이터 형식 변환이 반드시 필요한 경우에는 애플리케이션에서가 아니라 드라이버가 변환을 수행하도록 하는 것이 효율적입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 일반적으로 네트워크 버퍼에서 애플리케이션의 변수에 직접 데이터를 전달합니다. 데이터 변환을 수행하도록 드라이버에 요청하면 드라이버는 데이터를 버퍼링한 후 CPU 주기를 사용하여 데이터를 변환합니다.  
  
 프로그램 변수는 **text**, **ntext**및 **image** 데이터를 제외 하 고 열에서 전송 된 데이터를 저장할 수 있을 만큼 커야 합니다. 애플리케이션이 결과 집합 데이터를 검색한 후 해당 데이터를 수용하기에 너무 작은 변수에 데이터를 삽입하려고 하면 드라이버가 경고를 생성합니다. 이 경우 드라이버는 메시지에 사용할 메모리를 할당하게 되고 드라이버와 애플리케이션 모두 메시지 및 오류 처리를 위해 CPU 주기를 사용해야 합니다. 애플리케이션은 검색된 데이터를 수용할 수 있을 만큼 큰 변수를 할당하거나 SELECT 목록에서 SUBSTRING 함수를 사용하여 결과 집합의 열 크기를 줄여야 합니다.  
  
 SQL_C_DEFAULT를 사용하여 C 변수의 형식을 지정할 때는 주의를 기울여야 합니다. SQL_C_DEFAULT는 C 변수 형식이 열이나 매개 변수의 SQL 데이터 형식과 일치하도록 지정합니다. **Ntext**, **nchar**또는 **nvarchar** 열에 SQL_C_DEFAULT을 지정 하면 유니코드 데이터가 응용 프로그램으로 반환 됩니다. 유니코드 데이터를 처리하도록 애플리케이션이 코딩되지 않은 경우 이로 인해 여러 가지 문제가 발생할 수 있습니다. **Uniqueidentifier** (SQL_GUID) 데이터 형식에는 동일한 유형의 문제가 발생할 수 있습니다.  
  
 **text**, **ntext**및 **image** 데이터는 일반적으로 너무 커서 단일 프로그램 변수에 맞지 않으며 일반적으로 **SQLBindCol**대신 **SQLGetData** 를 사용 하 여 처리 됩니다. 서버 커서를 사용할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 행이 인출 될 때 바인딩되지 않은 **text**, **ntext**또는 **image** 열에 대 한 데이터를 전송 하지 않도록 최적화 되어 있습니다. **Text**, **ntext**또는 **image** 데이터는 응용 프로그램이 열에 대해 **SQLGetData** 를 발급할 때까지 서버에서 실제로 검색 되지 않습니다.  
  
 사용자가 커서를 위나 아래로 스크롤 하는 동안 **text**, **ntext**또는 **image** 데이터가 표시 되지 않도록 이러한 최적화를 응용 프로그램에 적용할 수 있습니다. 사용자가 행을 선택 하면 응용 프로그램에서 **SQLGetData** 를 호출 하 여 **text**, **ntext**또는 **image** 데이터를 검색할 수 있습니다. 이렇게 하면 사용자가 선택 하지 않은 행에 대해 **text**, **ntext**또는 **image** 데이터를 전송 하 고 대량의 데이터 전송을 저장할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;결과 처리](processing-results-odbc.md)  
  
  

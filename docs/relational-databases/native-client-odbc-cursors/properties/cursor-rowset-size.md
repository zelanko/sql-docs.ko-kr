---
title: 커서 로우셋 크기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f799722bfae35a714e740691e2cdc53e3155063
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302879"
---
# <a name="cursor-rowset-size"></a>커서 행 집합 크기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 커서는 한 번에 한 행씩만 인출하도록 제한되지 않습니다. **SQLFetch** 또는 [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)에 대한 각 호출에서 여러 행을 검색할 수 있습니다. Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 같은 클라이언트/서버 데이터베이스 작업을 할 때는 한 번에 여러 행을 인출하는 것이 효율적입니다. FETCH에서 반환되는 행 수를 행 집합 크기라고 하며 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)의 SQL_ATTR_ROW_ARRAY_SIZE 사용하여 지정됩니다.  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 행 집합 크기가 1보다 큰 커서를 블록 커서라고 합니다.  
  
 블록 커서를 위해 결과 집합 열을 바인딩하는 다음 두 가지 옵션이 있습니다.  
  
-   열 단위 바인딩  
  
     각 열이 변수 배열에 바인딩됩니다. 각 배열의 요소 수는 행 집합 크기와 같습니다.  
  
-   행 단위 바인딩  
  
     행의 모든 열에 대한 데이터와 표시기가 포함된 구조를 사용하여 배열이 작성됩니다. 배열의 구조 수는 행 집합 크기와 같습니다.  
  
 열 별 또는 행 별 바인딩을 사용 하는 경우 **SQLFetch** 또는 **SQLFetchScroll에** 대 한 각 호출 검색 된 행 집합에서 데이터바인딩된 배열을 채웁니다.  
  
 [SQLGetData는](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 블록 커서에서 열 데이터를 검색하는 데 사용할 수도 있습니다. **SQLGetData는** 한 번에 하나의 행을 작동하기 때문에 SQLGetData 를 호출하기 전에 행 집합의 특정 행을 현재 행으로 설정하려면 **SQLSetPos를** 호출해야 합니다. **SQLGetData**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 행 집합을 사용하여 전체 결과 집합을 신속하게 검색하는 최적화를 제공합니다. 이 최적화를 사용하려면 **SQLExecDirect** 또는 **SQLExecute가** 호출될 때 커서 특성을 기본값(정방향 전용, 읽기 전용, 행 집합 크기 = 1)으로 설정합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 기본 결과 집합을 설정합니다. 스크롤 없이 결과를 클라이언트로 전송하는 경우 이 방법이 서버 커서보다 더 효율적입니다. 문이 실행된 후 행 집합 크기를 늘리고 열 단위 또는 행 단위 바인딩을 사용합니다. 이렇게 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 하면 기본 결과 집합을 사용하여 결과 행을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트로 효율적으로 보내고 네이티브 클라이언트 ODBC 드라이버는 클라이언트의 네트워크 버퍼에서 행을 계속 가져옵니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서 속성](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  

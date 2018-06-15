---
title: 커서 행 집합 크기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 65a90b983e21925dd9406874279b5742f50a738b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32944788"
---
# <a name="cursor-rowset-size"></a>커서 행 집합 크기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC 커서는 한 번에 한 행씩만 인출하도록 제한되지 않습니다. 호출할 때마다 여러 행을 검색할 수 있습니다 **SQLFetch** 또는 [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)합니다. Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 같은 클라이언트/서버 데이터베이스 작업을 할 때는 한 번에 여러 행을 인출하는 것이 효율적입니다. 인출 시 반환 된 행 수가 행 집합 크기 라고 하며의 SQL_ATTR_ROW_ARRAY_SIZE를 사용 하 여 지정 된 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다.  
  
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
  
 열 단위 또는 행 단위 바인딩을 사용 되는 경우,를 호출할 때마다 **SQLFetch** 또는 **SQLFetchScroll** 바인딩된 배열이 검색 된 행 집합의 데이터로 채웁니다.  
  
 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 블록 커서에서 열 데이터 검색을 사용할 수도 있습니다. 때문에 **SQLGetData** 한 번에 하나의 행을 작동 **SQLSetPos** 호출을 호출 하기 전에 현재 행으로 행 집합의 특정 행을 설정 해야 **SQLGetData**합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 행 집합을 사용 하 여 전체 결과 집합을 신속 하 게 검색 하는 최적화를 제공 합니다. 이 최적화를 사용 하려면 커서 특성을 기본값으로 설정 (읽기 전용, 정방향 전용 행 집합 크기 = 1) 시간에 **SQLExecDirect** 또는 **SQLExecute** 호출 됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 기본 결과 집합을 설정 합니다. 스크롤 없이 결과를 클라이언트로 전송하는 경우 이 방법이 서버 커서보다 더 효율적입니다. 문이 실행된 후 행 집합 크기를 늘리고 열 단위 또는 행 단위 바인딩을 사용합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용 하 여 기본 결과 클라이언트에 결과 행을 효율적으로 보내도록 설정 하는 동안는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 클라이언트의 네트워크 버퍼에서 행을 지속적으로 끌어옵니다.  
  
## <a name="see-also"></a>관련 항목:  
 [커서 속성](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  

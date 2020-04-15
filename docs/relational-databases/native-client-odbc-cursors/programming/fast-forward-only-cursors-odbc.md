---
title: 빠른 전진 전용 커서 (ODBC) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50d79875e0f3f661c0a959f50ce68c4f2761d186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298423"
---
# <a name="fast-forward-only-cursors-odbc"></a>빠른 정방향 전용 커서(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스에 연결하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 정방향 전용 읽기 전용 커서에 대한 성능 최적화를 지원합니다. 빠른 정방향 전용 커서는 기본 결과 집합과 매우 유사한 방식으로 드라이버 및 서버에서 내부적으로 구현됩니다. 정방향 전용 커서는 높은 성능 외에도 다음과 같은 특성이 있습니다.  
  
-   [SQLGetData는](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 지원되지 않습니다. 결과 집합 열은 프로그램 변수에 바인딩되어야 합니다.  
  
-   서버에서 커서 끝을 감지하면 커서를 자동으로 닫습니다. 응용 프로그램은 여전히 [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) 또는 [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE)를 호출해야하지만 드라이버는 서버에 닫기 요청을 보낼 필요가 없습니다. 따라서 서버로의 네트워크 왕복이 줄어듭니다.  
  
 애플리케이션에서는 각 드라이버에 맞는 문 특성 SQL_SOPT_SS_CURSOR_OPTIONS를 사용하여 빠른 정방향 전용 커서를 요청합니다. SQL_CO_FFO로 설정하면 자동 인출 없이 빠른 정방향 전용 커서를 활성화합니다. SQL_CO_FFO_AF로 설정하면 자동 인출 옵션도 활성화됩니다. 오토페치에 대한 자세한 내용은 [ODBC 커서가 있는 자동 페치 사용을](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md)참조하십시오.  
  
 자동 인출 기능을 사용하는 빠른 정방향 전용 커서는 서버 왕복을 하나만 포함하는 작은 결과 집합을 검색하는 데 사용할 수 있습니다. 이 단계에서 *n은* 반환할 행 수입니다.  
  
1.  SQL_SOPT_SS_CURSOR_OPTIONS를 SQL_CO_FFO_AF로 설정합니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE *n* + 1로 설정합니다.  
  
3.  결과 열을 *n* + 1 요소의 배열에 바인딩합니다 *(n* + 1 행이 실제로 가져온 경우 안전합니다).  
  
4.  **SQLExecDirect** 또는 **SQLExecute를**통해 커서를 엽니다.  
  
5.  반환 상태가 SQL_SUCCESS 경우 **SQLFreeStmt** 또는 **SQLCloseCursor를** 호출하여 커서를 닫습니다. 행의 모든 데이터가 바인딩된 프로그램 변수에 포함됩니다.  
  
 이러한 단계를 통해 **SQLExecDirect** 또는 **SQLExecute는** 자동 가져오기 옵션을 사용하도록 설정한 커서 열기 요청을 보냅니다. 클라이언트의 해당 단일 요청에 대해 서버는 다음을 수행합니다.  
  
-   커서를 엽니다.  
  
-   결과 집합을 작성하고 행을 클라이언트에 보냅니다.  
  
-   행 집합 크기를 결과 집합의 행 수보다 1개 많은 수로 설정했으므로 서버가 커서의 끝을 발견하고 커서를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;커서 프로그래밍 세부 정보](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  

---
title: SQLFetch스크롤 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c75db1836b0c77c679c090a2d3e9454320872458
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300305"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLFetchScroll** 응용 프로그램에 데이터의 한 행 집합을 반환 합니다. 행 집합의 크기는 [SQLSetStmtAttr을](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)사용하여 설정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 다음과 같은 제한 사항으로 정의된 모든 가져오기 명령(예: SQL_FETCH_RELATIVE)을 지원합니다.  
  
-   문에 대해 정방향 전용 커서가 정의된 경우 SQL_FETCH_NEXT가 필요하며, 다른 방식으로 인출을 시도하면 오류가 반환됩니다.  
  
-   SQL_FETCH_BOOKMARK는 정적 및 키 집합 커서에 대해서만 지원됩니다.  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLFetchScroll 지원  
 날짜/시간 형식의 결과 열 값은 [SQL에서 C로의 변환에](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)설명된 대로 변환됩니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLFetchScroll 지원  
 **SQLFetchScroll는** 큰 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLFetch스크롤 함수](https://go.microsoft.com/fwlink/?LinkId=59343)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  

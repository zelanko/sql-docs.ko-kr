---
title: "ODBC 커서로 자동 인출 사용 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9b0dd154b1f8a4dd791dfc111dacaa750a66da96
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="using-autofetch-with-odbc-cursors"></a>ODBC 커서로 자동 인출 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  인스턴스에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 모든 서버 커서 유형을 사용 하는 경우 자동 인출 옵션을 지원 합니다. 자동 인출을 사용는 **SQLExecute** 또는 **SQLExecDirect** 하면 커서 함수 역시 암시적 [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) 함수도 있습니다. 문 실행의 일부로 첫 번째 행 집합을 구성하는 행이 바인딩된 응용 프로그램 변수에 반환되므로 네트워크를 통해 다시 서버로 왕복할 필요가 없습니다. [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 때 지원 되지 않습니다 자동 인출 옵션을 사용할 수 있습니다; 결과 집합 열을 프로그램 변수에 바인딩해야 합니다.  
  
 응용 프로그램은 드라이버별 SQL_SOPT_SS_CURSOR_OPTIONS 문 특성을 SQL_CO_AF로 설정하여 자동 인출을 요청합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [커서 프로그래밍 정보 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  

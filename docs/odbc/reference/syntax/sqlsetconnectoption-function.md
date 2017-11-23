---
title: "SQLSetConnectOption 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLSetConnectOption
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetConnectOption
helpviewer_keywords: SQLSetConnectOption function [ODBC]
ms.assetid: 8cd2c2a2-25c8-4aff-951c-b593bbfc90ad
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b133c5a34dd37f02dd930d2a035c6b69ea49b093
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 ODBC 3에서*.x*, ODBC 2.0 함수 **SQLSetConnectOption** 로 대체 되었습니다 **SQLSetConnectAttr**합니다. 자세한 내용은 참조 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.  
  
> [!NOTE]  
>  어떤 드라이버 관리자는이 함수를 경우 맵을 ODBC 2에 대 한 자세한 내용은*.x* 응용 프로그램이 ODBC 3 작동*.x* 드라이버 참조 [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>주의  
 참조 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우.  
  
> [!NOTE]  
>  ODBC 3.8에 도입 된 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성에서 지원 되지 않습니다 **SQLSetConnectOption**합니다. 연결 핸들에서 비동기 작업을 사용 하는 응용 프로그램 사용 해야 **SQLSetConnectAttr**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

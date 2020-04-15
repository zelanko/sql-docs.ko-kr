---
title: SQLSetConnect옵션 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectOption
helpviewer_keywords:
- SQLSetConnectOption function [ODBC]
ms.assetid: 8cd2c2a2-25c8-4aff-951c-b593bbfc90ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 263b15cb75fb5c0c7c1d7aa630a8da171b9765a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301598"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 함수
**규칙**  
 버전 도입: ODBC 1.0 표준 규정 준수: 더 이상 사용되지 않는  
  
 **요약**  
 ODBC 3 *.x에서*ODBC 2.0 함수 **SQLSetConnectOption이** **SQLSetConnectAttr로**대체되었습니다. 자세한 내용은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)을 참조하세요.  
  
> [!NOTE]
>  ODBC 2 *.x* 응용 프로그램이 ODBC 3 *.x* 드라이버로 작업할 때 드라이버 관리자가 이 함수를 매핑하는 작업에 대한 자세한 내용은 [더 이상 사용되지 않은 함수 매핑"을](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)참조하십시오.  
  
## <a name="remarks"></a>설명  
 [64비트](../../../odbc/reference/odbc-64-bit-information.md)운영 체제에서 응용 프로그램이 실행되는 경우 ODBC 64비트 정보를 참조하십시오.  
  
> [!NOTE]  
>  ODBC 3.8에서 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성은 **SQLSetConnectOption에서**지원되지 않습니다. 연결 핸들에서 비동기 작업을 사용하는 응용 프로그램은 **SQLSetConnectAttr**을 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

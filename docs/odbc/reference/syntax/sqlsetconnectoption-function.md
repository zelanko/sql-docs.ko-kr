---
title: SQLSetConnectOption 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2a4965fedc7da47751742e863119b818a9fcba9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646361"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 함수
**규칙**  
 버전에 도입 되었습니다: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 ODBC 3에서 *.x*, ODBC 2.0 함수 **SQLSetConnectOption** 바뀌었습니다 **SQLSetConnectAttr**합니다. 자세한 내용은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)을 참조하세요.  
  
> [!NOTE]  
>  새로운 드라이버 관리자는이 함수를 경우 맵을 ODBC 2 대 한 자세한 내용은 *.x* 는 ODBC 3을 사용 하 여 응용 프로그램이 작동 *.x* 드라이버를 참조 하세요. [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>Remarks  
 참조 [ODBC 64-Bit 정보](../../../odbc/reference/odbc-64-bit-information.md)이면 응용 프로그램을 64 비트 운영 체제에서 실행 됩니다.  
  
> [!NOTE]  
>  ODBC 3.8에 도입 된 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성에서 지원 되지 않습니다 **SQLSetConnectOption**합니다. 연결 핸들에서 비동기 작업을 사용 하는 응용 프로그램을 사용 해야 합니다 **SQLSetConnectAttr**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

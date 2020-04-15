---
title: SQLGetConnect옵션 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94a29637365862990ea067f663023fae04a7af3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285573"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 함수
**규칙**  
 버전 도입: ODBC 1.0 표준 규정 준수: 더 이상 사용되지 않는  
  
 **요약**  
 ODBC *3.x에서*ODBC *2.x* 함수 **SQLGetConnectOption이** **SQLGetConnectAttr로**대체되었습니다. 자세한 내용은 [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)을 참조하십시오.  
  
> [!NOTE]
>  ODBC *2.x* 응용 프로그램이 ODBC *3.x* 드라이버로 작업할 때 드라이버 관리자가 이 함수를 매핑하는 방법에 대한 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침의 [더 이상 사용되지 않은 함수 매핑을](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 참조하십시오.  
> 
> [!NOTE]
>  ODBC 3.8에서 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성은 **SQLGetConnectOption에서**지원되지 않습니다. 연결 핸들에서 비동기 연산을 사용하는 응용 프로그램은 **SQLGetConnectAttr**을 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

---
title: "SQLGetConnectOption 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5c66629eb9c2de276fd26179086b4aedb812863b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 ODBC 3에서*.x*, ODBC 2*.x* 함수 **SQLGetConnectOption** 로 대체 되었습니다 **SQLGetConnectAttr**합니다. 자세한 내용은 참조 [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)합니다.  
  
> [!NOTE]  
>  어떤 드라이버 관리자는이 함수를 경우 맵을 ODBC 2에 대 한 자세한 내용은*.x* 응용 프로그램이 ODBC 3 작동*.x* 드라이버 참조 [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
  
> [!NOTE]  
>  ODBC 3.8에 도입 된 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성에서 지원 되지 않습니다 **SQLGetConnectOption**합니다. 연결 핸들에서 비동기 작업을 사용 하는 응용 프로그램 사용 해야 **SQLGetConnectAttr**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

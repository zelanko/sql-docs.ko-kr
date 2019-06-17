---
title: SQLGetConnectOption 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30d91302161b236cee5634196bea33f61411f046
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259573"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. 사용되지 않음  
  
 **요약**  
 ODBC 3에서 *.x*, ODBC 2 *.x* 함수 **SQLGetConnectOption** 바뀌었습니다 **SQLGetConnectAttr**합니다. 자세한 내용은 [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)합니다.  
  
> [!NOTE]
>  새로운 드라이버 관리자는이 함수를 경우 맵을 ODBC 2 대 한 자세한 내용은 *.x* 는 ODBC 3을 사용 하 여 응용 프로그램이 작동 *.x* 드라이버를 참조 하세요. [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)부록 g: 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
> 
> [!NOTE]
>  ODBC 3.8에 도입 된 SQL_ASYNC_DBC_FUNCTION_ENABLE 특성에서 지원 되지 않습니다 **SQLGetConnectOption**합니다. 연결 핸들의 비동기 작업을 사용 하는 응용 프로그램을 사용 해야 합니다 **SQLGetConnectAttr**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

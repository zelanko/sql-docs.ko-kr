---
title: SQLSetScrollOptions 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a85caefadb54c3db2716c4db18b504e02da996
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342943"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: 사용되지 않음  
  
 **요약**  
 *Odbc 3.x*에서 odbc 2.0 함수 **SQLSetScrollOptions** 은 **SQLGetInfo** 및 **SQLSetStmtAttr**에 대 한 호출로 대체 되었습니다.  
  
> [!NOTE]
>  ODBC *2.x 응용 프로그램이* odbc *3.x 드라이버를* 사용할 때 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용은 부록 G에서 [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 을 참조 하세요. 이전 버전과의 호환성을 위한 드라이버 지침  
> 
> [!NOTE]
>  드라이버 관리자가 **SQLSetScrollOptions**을 지원 하지 *않는 ODBC 2.x* 드라이버를 사용 하 여 작동 하는 응용 프로그램에 대 한 **SQLSetScrollOptions** 를 매핑하는 경우 드라이버 관리자는 SQL_ATTR_ROW_ 아닌 SQL_ROWSET_SIZE 문 옵션을 설정 합니다. ARRAY_SIZE 문 특성을 **SQLSetScrollOption**의 *RowsetSize* 인수에 추가할 수 있습니다. 결과적으로 **Sqlfetch** 또는 **sqlfetchscroll**을 호출 하 여 여러 행을 인출 하는 경우 응용 프로그램에서 **SQLSetScrollOptions** 를 사용할 수 없습니다. **Sqlextendedfetch**를 호출 하 여 여러 행을 인출 하는 경우에만 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)를 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

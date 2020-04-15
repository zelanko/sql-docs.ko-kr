---
title: SQLSet스크롤옵션 기능 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 056fc203581e1d5d8323b09ac62d692093d8c0f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287272"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 함수
**규칙**  
 버전 도입: ODBC 1.0 표준 규정 준수: 더 이상 사용되지 않는  
  
 **요약**  
 ODBC *3.x에서*ODBC 2.0 함수 **SQLSetScrollOptions는** **SQLGetInfo** 및 **SQLSetStmtAttr**에 대한 호출로 대체되었습니다.  
  
> [!NOTE]
>  ODBC *2.x* 응용 프로그램이 ODBC *3.x* 드라이버로 작업할 때 드라이버 관리자가 이 함수를 매핑하는 방법에 대한 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침의 [더 이상 사용되지 않은 함수 매핑을](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 참조하십시오.  
> 
> [!NOTE]
>  드라이버 **관리자가 SQLSetScrollOptions를** 지원하지 않는 ODBC *3.x* 드라이버로 작업하는 응용 프로그램에 대해 **SQLSetScrollOptions를**매핑할 때 드라이버 관리자는 SQL_ATTR_ROW_ARRAY_SIZE 문 특성이 아닌 SQL_ROWSET_SIZE 명령문 옵션을 **SQLSetScrollOption의** *RowsetSize* 인수로 설정합니다. 따라서 SQLFetch스크롤 에 대한 호출로 여러 행을 가져올 때 응용 프로그램에서 **SQLFetchScroll** **SQLSetScroll 옵션을** 사용할 수 없습니다. **SQLFetch** **SQLExtendedFetch**에 대한 호출로 여러 행을 가져올 때만 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 응용 프로그램이 64비트 운영 체제에서 실행되는 경우 [ODBC 64비트 정보를](../../../odbc/reference/odbc-64-bit-information.md)참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

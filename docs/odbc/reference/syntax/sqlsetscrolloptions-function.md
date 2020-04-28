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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 056fc203581e1d5d8323b09ac62d692093d8c0f5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287272"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: 사용 되지 않음  
  
 **요약**  
 *Odbc 3.x에서 odbc 2.0*함수 **SQLSetScrollOptions** 은 **SQLGetInfo** 및 **SQLSetStmtAttr**에 대 한 호출로 대체 되었습니다.  
  
> [!NOTE]
>  ODBC *2.x 응용 프로그램에서 odbc 2.x* *드라이버를* 사용할 때 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침에서 [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 을 참조 하세요.  
> 
> [!NOTE]
>  드라이버 관리자가 **SQLSetScrollOptions**을 지원 하지 *않는 ODBC 2.x* 드라이버를 사용 하 여 작동 하는 응용 프로그램에 대해 **SQLSetScrollOptions** 를 매핑하는 경우 드라이버 관리자는 SQL_ATTR_ROW_ARRAY_SIZE statement 특성이 아닌 SQL_ROWSET_SIZE 문 옵션을 **SQLSetScrollOption**의 *RowsetSize* 인수로 설정 합니다. 결과적으로 **Sqlfetch** 또는 **sqlfetchscroll**을 호출 하 여 여러 행을 인출 하는 경우 응용 프로그램에서 **SQLSetScrollOptions** 를 사용할 수 없습니다. **Sqlextendedfetch**를 호출 하 여 여러 행을 인출 하는 경우에만 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)

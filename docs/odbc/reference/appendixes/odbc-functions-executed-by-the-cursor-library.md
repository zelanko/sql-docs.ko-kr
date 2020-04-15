---
title: 커서 라이브러리에서 실행되는 ODBC 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], functions
- functions [ODBC], cursor library
- ODBC functions [ODBC], cursor library
- ODBC cursor library [ODBC], functions
ms.assetid: 2f1d3386-7e59-4d55-a5b4-3440b61343a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70fb48a8764a913ea4c2376c1a44bcd8712e7d29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298233"
---
# <a name="odbc-functions-executed-by-the-cursor-library"></a>커서 라이브러리에 의해 실행되는 ODBC 함수
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 커서 라이브러리는 다음 기능을 실행합니다. 응용 프로그램이 이 목록의 함수를 호출하면 드라이버 관리자는 드라이버가 아닌 커서 라이브러리를 호출합니다. 커서 라이브러리는 함수를 실행할 때 드라이버를 호출할 수 있습니다.  
  
|||  
|-|-|  
|**SQLBindCol**|**SQLGetStmt옵션**|  
|**SQLBindParam**|**SQLNativeSql**|  
|**SQLBindParameter**|**SQLNumParams**|  
|**SQLCloseCursor**|**SQLParam옵션**|  
|**SQLEndTran**|**SQLRowCount**|  
|**SQLExtendedFetch**|**SQLSetConnectAttr**|  
|**SQLFetchScroll**|**SQLSet연결옵션**|  
|**SQLFreeHandle**|**SQLSetDescField**|  
|**SQLFreeStmt**|**SQLSetDescRec**|  
|**SQLGetData**|**SQLSetPos**|  
|**SQLGetDescField**|**SQLSet스크롤 옵션**|  
|**SQLGetDescRec**|**SQLSetStmtAttr**|  
|**SQLGetFunctions**|**SQLSetStmt옵션**|  
|**SQLGetInfo**|**SQLTransact**|  
|**SQLGetStmtAttr**||

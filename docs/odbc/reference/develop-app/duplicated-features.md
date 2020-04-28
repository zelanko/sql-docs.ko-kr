---
title: 중복 된 기능 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00f5529cfbfacebcad78a0a4433e84f34034694a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300483"
---
# <a name="duplicated-features"></a>중복된 기능
다음 ODBC 2.x *함수는 odbc* *2.x 함수에서* 중복 되었습니다. 따라서 *odbc 2.x 함수는* odbc 2.x에서 더 이상 사용 되지 *않습니다.* ODBC 3.x 함수를 대체 함수 라고 *합니다.*  
  
 응용 프로그램에서 사용 되지 않는 ODBC *2.x 함수를* 사용 하 고 기본 드라이버가 odbc 3.x 드라이버 *이면* 드라이버 관리자는 함수 호출을 해당 대체 함수에 매핑합니다. 이 규칙의 유일한 예외는 **Sqlextendedfetch**입니다. 다음 표 끝에 있는 각주를 참조 하십시오. 이러한 매핑에 대 한 자세한 내용은 부록 G에서 [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) : 이전 버전과의 호환성을 위한 드라이버 지침을 참조 하세요.  
  
 응용 프로그램에서 대체 함수를 사용 하 고 기본 드라이버가 ODBC 2.x 드라이버 *이면 드라이버 관리자* 는 함수 호출을 해당 하는 사용 되지 않는 함수에 매핑합니다.  
  
|ODBC *2.x* 함수|ODBC *3.x* 함수|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**Sqlextendedfetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] **Sqlextendedfetch** 함수는 중복 된 기능입니다. **Sqlfetchscroll** 은 ODBC 3.x에서 동일한 기능을 *제공 합니다.* 그러나 ODBC 3.x 드라이버를 사용할 경우에는 드라이버 관리자가 **Sqlextendedfetch** 를 **sqlextendedfetch** 에 매핑하지 *않습니다.* 자세한 내용은 부록 G: 드라이버 [관리자](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) 의 이전 버전과의 호환성에 대 한 지침을 참조 하세요. 드라이버 관리자 *는 ODBC 2.x* 드라이버에서 이동할 때 **Sqlfetchscroll** 를 **sqlfetchscroll** 에 매핑합니다.  
  
> [!NOTE]
>  **Sqlbindparam 함수와** 함수는 특수 한 경우입니다. **Sqlbindparam 함수와** 는 중복 된 기능입니다. 이 함수 *는 ODBC 2.x* 함수는 아니지만 오픈 그룹 및 ISO 표준에 있는 함수입니다. 이 함수에서 제공 하는 기능은 **SQLBindParameter**에 의해 완전히 스페이스가 됩니다. 결과적으로, 드라이버 관리자는 기본 드라이버가 ODBC 3.x 드라이버 일 때 **sqlbindparam 함수와** 에 대 한 호출을 **SQLBindParameter** 에 *매핑합니다.* 그러나 기본 *드라이버가 ODBC 2.x* 드라이버 이면 드라이버 관리자는이 매핑을 수행 하지 않습니다.

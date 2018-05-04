---
title: 복제 기능 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55faa01b16331870c4539e290e218838e4d9e381
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="duplicated-features"></a>중복 된 기능
다음 ODBC 2입니다. *x* 함수 ODBC 3에 의해 복제 된 했습니다. *x* 함수입니다. 결과적으로 ODBC 2. *x* ODBC 3에서 함수는 사용 되지 않습니다. *x*합니다. ODBC 3입니다. *x* 함수는 대체 함수 라고 합니다.  
  
 응용 프로그램 사용 하는 경우 사용 되지 않는 ODBC 2. *x* 함수 및 기본 드라이버는 ODBC 3. *x* 드라이버를 드라이버 관리자는 해당 대체 함수에 대 한 함수 호출에 매핑합니다. 이 규칙에 대 한 유일한 예외 **SQLExtendedFetch**합니다. (다음 테이블의 끝에 각주 참조). 이러한 매핑에 대 한 자세한 내용은 참조 [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
  
 응용 프로그램 대체 함수 및 기본 드라이버를 사용 하는 경우는 ODBC 2입니다. *x* 드라이버를 드라이버 관리자는 해당 사용 되지 않는 함수에 대 한 함수 호출에 매핑합니다.  
  
|ODBC 2입니다. *x* 함수|ODBC 3입니다. *x* 함수|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 함수 **SQLExtendedFetch** 복제 기능은; **SQLFetchScroll** ODBC 3에서 동일한 기능을 제공 합니다. *x*합니다. 그러나 드라이버 관리자 매핑되지 않는 **SQLExtendedFetch** 를 **SQLFetchScroll** ODBC 3에 대 한 라인으로 전환 하는 경우. *x* 드라이버입니다. 자세한 내용은 참조 [the 드라이버 관리자의 용도](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다. 드라이버 관리자 매핑합니다 **SQLFetchScroll** 를 **SQLExtendedFetch** ODBC 2에 대 한 라인으로 전환 하는 경우. *x* 드라이버입니다.  
  
> [!NOTE]  
>  함수 **SQLBindParam** 는 특별 한 경우. **SQLBindParam** 기능을 복제 합니다. 이 ODBC 2 *.x* 함수, 했지만 Open Group 및 ISO 표준에 존재 하는 함수입니다. 이 함수에 의해 제공 되는 기능에 따라 완전히 포함 됩니다. **SQLBindParameter**합니다. 결과적으로, 드라이버 관리자에 대 한 호출을 매핑합니다 **SQLBindParam** 를 **SQLBindParameter** 때 기본 드라이버는 ODBC 3. *x* 드라이버입니다. 그러나 기본 드라이버는 ODBC 2는 *.x* 드라이버를 드라이버 관리자에서이 매핑을 수행 하지 않습니다.

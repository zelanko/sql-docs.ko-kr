---
title: 중복 기능 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ca73b5b9b41c99bd6db8e6181fa3582cae47c1d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046898"
---
# <a name="duplicated-features"></a>중복된 기능
다음 ODBC *2.x* ODBC에서 중복 된 함수 *3.x* 함수입니다. 결과적으로 ODBC *2.x* 함수는 ODBC에서 사용 되지 않는 *3.x*합니다. ODBC *3.x* 함수를 대체 함수 라고 합니다.  
  
 응용 프로그램에서 사용 되지 않는 ODBC를 사용 하는 경우 *2.x* 함수 및 기본 드라이버는 ODBC *3.x* 드라이버를 드라이버 관리자를 해당 대체 함수에 대 한 함수 호출을 매핑합니다. 이 규칙의 유일한 예외는 **SQLExtendedFetch**합니다. (끝에 다음 표에서 각주 참조). 이러한 매핑에 대 한 자세한 내용은 참조 하세요. [사용 되지 않는 함수 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 부록 g:에서 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
  
 대체 함수를 사용 하는 응용 프로그램 기본 드라이버는 ODBC 시점과 *2.x* 드라이버를 드라이버 관리자 함수 호출을 해당 하는 사용 되지 않는 함수를 매핑합니다.  
  
|ODBC *2.x* 함수|ODBC *3.x* 함수|  
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
  
 [1] 함수 **SQLExtendedFetch** 중복 기능은; **SQLFetchScroll** ODBC에서 동일한 기능을 제공 *3.x*합니다. 그러나 드라이버 관리자 매핑되지 **SQLExtendedFetch** 하 **SQLFetchScroll** ODBC에 대 한 경우 *3.x* 드라이버. 자세한 내용은 [the Driver Manager 용도](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) 부록 g:에서 이전 버전과 호환성에 대 한 드라이버 지침입니다. 드라이버 관리자 매핑합니다 **SQLFetchScroll** 하 **SQLExtendedFetch** ODBC에 대 한 경우 *2.x* 드라이버입니다.  
  
> [!NOTE]
>  함수 **SQLBindParam** 는 특별 한 경우. **SQLBindParam** 중복 된 기능입니다. 이 ODBC *2.x* 함수 하지만 Open Group 및 ISO 표준에 존재 하는 함수입니다. 이 함수에서 제공 하는 기능에 따라 완전히 포함 됩니다. **SQLBindParameter**합니다. 결과적으로 드라이버 관리자에 대 한 호출을 매핑합니다 **SQLBindParam** 하 **SQLBindParameter** 때 기본 드라이버는 ODBC *3.x* 드라이버입니다. 그러나 기본 드라이버 경우 ODBC *2.x* 드라이버를 드라이버 관리자는이 매핑을 수행 하지 않습니다.

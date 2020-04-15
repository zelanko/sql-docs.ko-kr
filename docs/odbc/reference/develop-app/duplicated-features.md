---
title: 중복 된 기능 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300483"
---
# <a name="duplicated-features"></a>중복된 기능
다음 ODBC *2.x* 함수는 ODBC *3.x* 함수에 의해 복제되었습니다. 결과적으로 ODBC *2.x* 함수는 ODBC *3.x에서*더 이상 사용되지 않습니다. ODBC *3.x* 함수를 대체 함수라고 합니다.  
  
 응용 프로그램이 더 이상 사용되지 않은 ODBC *2.x* 함수를 사용하고 기본 드라이버가 ODBC *3.x* 드라이버인 경우 드라이버 관리자는 함수 호출을 해당 대체 함수에 매핑합니다. 이 규칙의 유일한 예외는 **SQLExtendedFetch**입니다. (다음 표의 끝에 있는 각주를 참조한다.) 이러한 매핑에 대한 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침의 [더 이상 사용되지 않음된 함수 매핑을](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) 참조하십시오.  
  
 응용 프로그램이 대체 함수를 사용하고 기본 드라이버가 ODBC *2.x* 드라이버인 경우 드라이버 관리자는 함수 호출을 해당 더 이상 사용되지 않은 함수에 매핑합니다.  
  
|ODBC *2.x* 기능|ODBC *3.x* 기능|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAlloc핸들**|  
|**SQLAllocEnv**|**SQLAlloc핸들**|  
|**SQLAllocStmt**|**SQLAlloc핸들**|  
|**SQLCol속성**|**SQLColAttribute**|  
|**SQL오류**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQL프리엔프**|**SQLFreeHandle**|  
|**SQLGet연결 옵션**|**SQLGetConnectAttr**|  
|**SQLGetStmt옵션**|**SQLGetStmtAttr**|  
|**SQLParam옵션**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSet연결옵션**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmt옵션**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] **SQLExtendedFetch** 함수는 중복된 기능입니다. **SQLFetchScroll는** ODBC *3.x .* 그러나 드라이버 관리자는 ODBC *3.x* 드라이버에 대해 갈 때 **SQLExtendedFetch를** **SQLFetchScroll에** 매핑하지 않습니다. 자세한 내용은 부록 G: 이전 버전과의 호환성에 대한 드라이버 지침에서 [드라이버 관리자가 수행하는 작업을](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) 참조하십시오. 드라이버 관리자는 ODBC *2.x* 드라이버에 대해 갈 때 **SQLExtendedFetch를** **SQLExtendedFetch에** 매핑합니다.  
  
> [!NOTE]
>  함수 **SQLBindParam은** 특별한 경우입니다. **SQLBindParam은** 중복된 기능입니다. 이것은 ODBC *2.x* 함수가 아니라 Open 그룹 및 ISO 표준에 있는 함수입니다. 이 함수에서 제공하는 기능은 **SQLBindParameter**. 결과적으로 드라이버 관리자는 기본 드라이버가 ODBC *3.x* 드라이버인 경우 **SQLBindParam에** 대한 호출을 **SQLBindParam에** 매핑합니다. 그러나 기본 드라이버가 ODBC *2.x* 드라이버인 경우 드라이버 관리자는 이 매핑을 수행하지 않습니다.

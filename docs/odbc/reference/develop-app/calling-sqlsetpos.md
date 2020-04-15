---
title: SQLSetPos 호출 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46cfbb4e2e6b60f620cd7e38272bf9308ece91bc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306244"
---
# <a name="calling-sqlsetpos"></a>SQLSetPos 호출
ODBC *2.x에서*행 상태 배열에 대한 포인터는 **SQLExtendedFetch**에 대한 인수였습니다. 행 상태 배열은 나중에 **SQLSetPos**에 대한 호출에 의해 업데이트되었습니다. 일부 드라이버는 이 배열이 **SQLExtendedFetch** 와 **SQLSetPos**간에 변경되지 않는다는 사실에 의존했습니다. ODBC *3.x에서*상태 배열에 대한 포인터는 설명자 필드이므로 응용 프로그램이 다른 배열을 가리키도록 쉽게 변경할 수 있습니다. ODBC *3.x* 응용 프로그램이 ODBC *2.x* 드라이버로 작업하지만 **SQLSetStmtAttr을** 호출하여 배열 상태 포인터를 설정하고 **SQLFetchScroll를** 호출하여 데이터를 가져오려고 호출하는 경우 문제가 될 수 있습니다. 드라이버 관리자는 **SQLExtendedFetch에**대한 호출 시퀀스로 매핑합니다. 다음 코드에서는 드라이버 관리자가 ODBC *2.x* 드라이버로 작업할 때 두 번째 **SQLSetStmtAttr** 호출을 매핑할 때 일반적으로 오류가 발생합니다.  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 **SQLExtendedFetch에**대한 호출 사이에 ODBC *2.x에서* 행 상태 포인터를 변경할 방법이 없는 경우 오류가 발생합니다. 대신 드라이버 관리자는 ODBC *2.x* 드라이버로 작업할 때 다음 단계를 수행합니다.  
  
1.  내부 드라이버 관리자 플래그 *fSetPosError를* TRUE로 초기화합니다.  
  
2.  응용 프로그램이 **SQLFetchScroll를**호출하면 드라이버 관리자는 *fSetPosError를* FALSE로 설정합니다.  
  
3.  응용 프로그램이 **SQLSetStmtAttr을** 호출하여 SQL_ATTR_ROW_STATUS_PTR 설정하면 드라이버 관리자는 *fSetPosError를* TRUE와 동일하게 설정합니다.  
  
4.  응용 프로그램이 **SQLSetPos를**호출할 때 *fSetPosErrortrue와* 같음으로 드라이버 관리자는 SQLSTATE HY011(특성을 지금 설정할 수 없음)으로 SQL_ERROR 발생시켜 응용 프로그램이 행 상태 포인터를 변경한 후 **SQLFetchScroll**을 호출하기 전에 **SQLSetPos를** 호출하려고 했음을 나타냅니다.

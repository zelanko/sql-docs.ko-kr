---
title: "SQLSetPos 호출 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 434031a496faae19ee37b8273341cc0ede6d0313
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlsetpos"></a>SQLSetPos 호출
Odbc 2. *x*, 행 상태 배열이에 대 한 포인터를 인수 했습니다 **SQLExtendedFetch**합니다. 호출 하 여 나중에 수정한 행 상태 배열이 **SQLSetPos**합니다. 일부 드라이버가이 배열 간에 변경 되지 않으므로 있다는 사실을 했었다면 **SQLExtendedFetch** 및 **SQLSetPos**합니다. Odbc 3. *x*, 상태 배열에 대 한 포인터는 설명자 필드를 이며 따라서 응용 프로그램이 쉽게 변경할 수 있습니다 다른 배열로 가리키도록 합니다. 이 경우 ODBC 3 문제가 될 수 있습니다. *x* 응용 프로그램이 작동 ODBC 2. *x* 드라이버를 호출 하는 있지만 **SQLSetStmtAttr** 배열 상태 포인터가 설정 하려면 하며 호출 **SQLFetchScroll** 데이터를 인출 합니다. 드라이버 관리자에 대 한 호출의 시퀀스로 매핑합니다 **SQLExtendedFetch**합니다. 다음 코드에서 오류가 일반적으로 발생 드라이버 관리자는 두 번째 매핑할 때 **SQLSetStmtAttr** ODBC 2 작업 시 호출할*.x* 드라이버:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 ODBC 2에서 행 상태 포인터를 변경할 수 없으므로 있는 경우는 오류가 발생할 것입니다. *x* 호출 간에 **SQLExtendedFetch**합니다. ODBC 2 작업할 때 드라이버 관리자는 다음 단계를 수행 하는 대신,*.x* 드라이버:  
  
1.  내부 드라이버 관리자 플래그를 초기화 *fSetPosError* TRUE로 합니다.  
  
2.  응용 프로그램 호출 하는 경우 **SQLFetchScroll**를 설정 하는 드라이버 관리자 *fSetPosError* FALSE로 합니다.  
  
3.  응용 프로그램 호출 하는 경우 **SQLSetStmtAttr** 드라이버 관리자 설정 SQL_ATTR_ROW_STATUS_PTR을 설정 하려면 *fSetPosError* 같은 toTRUE 합니다.  
  
4.  응용 프로그램 호출 하는 경우 **SQLSetPos**와 *fSetPosError* TRUE, 드라이버 관리자와 같음 SQLSTATE HY011 포함 된 sql_error가 발생 시킵니다 (특성 지금 설정할 수 없습니다) 임을 나타내는 응용 프로그램 호출 하려고 **SQLSetPos** 행 상태 포인터를 변경한 후 있지만 호출 하기 전에 **SQLFetchScroll**합니다.


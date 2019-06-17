---
title: SQLSetPos를 호출 합니다. | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70d574f867934af87ac7b5071b7f30bc9e89bccf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199440"
---
# <a name="calling-sqlsetpos"></a>SQLSetPos 호출
Odbc 2. *x*, 행 상태 배열에 대 한 포인터를 인수로 **SQLExtendedFetch**합니다. 호출 하 여 나중에 수정한 행 상태 배열이 **SQLSetPos**합니다. 일부 드라이버는이 배열 간에 변경 되지 않으므로 의존 **SQLExtendedFetch** 하 고 **SQLSetPos**합니다. Odbc 3. *x*상태 배열에 대 한 포인터는 설명자 필드 이며 따라서 응용 프로그램 쉽게 변경할 수 있습니다 다른 배열로 가리키도록 합니다. 이 경우 ODBC 3는 문제를 수 있습니다. *x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 합니다. *x* 드라이버 호출 하지만 **SQLSetStmtAttr** 배열 상태 포인터가 설정 하며 호출 **SQLFetchScroll** 데이터를 인출 합니다. 드라이버 관리자에 대 한 호출 시퀀스로 매핑합니다 **SQLExtendedFetch**합니다. 다음 코드에서는 일반적으로 될 때 오류가 발생 하 드라이버 관리자를 두 번째 매핑합니다 **SQLSetStmtAttr** 는 ODBC 2를 사용 하 여 작업 시 호출할 *.x* 드라이버:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 ODBC 2에 대 한 포인터 행 상태를 변경할 수 없는 경우 오류가 발생 합니다. *x* 호출 사이 **SQLExtendedFetch**합니다. ODBC 2를 사용 하 여 작업할 때 드라이버 관리자는 다음 단계를 수행 하는 대신 *.x* 드라이버:  
  
1.  내부 드라이버 관리자 플래그를 초기화 *fSetPosError* TRUE로 합니다.  
  
2.  응용 프로그램 호출 하는 경우 **SQLFetchScroll**를 설정 하는 드라이버 관리자 *fSetPosError* FALSE로 합니다.  
  
3.  응용 프로그램을 호출할 때 **SQLSetStmtAttr** SQL_ATTR_ROW_STATUS_PTR을 설정 하려면 드라이버 관리자는 다음과 같이 설정 됩니다. *fSetPosError* 같은 toTRUE 합니다.  
  
4.  응용 프로그램을 호출할 때 **SQLSetPos**를 사용 하 여 *fSetPosError* 를 TRUE로 드라이버 관리자는 동일한 SQLSTATE HY011를 사용 하 여 SQL_ERROR를 발생 시킵니다. (특성 지금 설정할 수 없습니다) 나타내는 응용 프로그램 호출 하려고 **SQLSetPos** 행 상태 포인터를 변경한 후 하지만 호출 하기 전에 **SQLFetchScroll**합니다.

---
title: SQLSetPos 호출 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306244"
---
# <a name="calling-sqlsetpos"></a>SQLSetPos 호출
ODBC 2.x에서 행 상태 배열에 *대 한 포인터*는 **sqlextendedfetch**에 대 한 인수입니다. 나중에 **SQLSetPos**를 호출 하 여 행 상태 배열을 업데이트 했습니다. 일부 드라이버는이 배열이 **Sqlextendedfetch** 와 **SQLSetPos**사이에서 변경 되지 않는다는 사실에 의존 했습니다. *ODBC 3.x에서 상태*배열에 대 한 포인터는 설명자 필드 이므로 응용 프로그램에서 다른 배열을 가리키도록 쉽게 변경할 수 있습니다. ODBC *3.x 응용 프로그램* 에서 odbc *2.x 드라이버를* 사용 하 고 있지만 배열 상태 포인터를 설정 하 고 **sqlfetchscroll** 을 호출 하 여 데이터를 **인출 하는** 경우에는 문제가 발생할 수 있습니다. 드라이버 관리자는이를 **Sqlextendedfetch**에 대 한 호출 시퀀스로 매핑합니다. 다음 코드에서는 드라이버 관리자 *가 ODBC 2.x* 드라이버를 사용할 때 두 번째 **SQLSetStmtAttr** 호출을 매핑할 때 일반적으로 오류가 발생 합니다.  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 **Sqlextendedfetch** *호출 사이에서* ODBC 2.x의 행 상태 포인터를 변경할 방법이 없는 경우 오류가 발생 합니다. 대신, 드라이버 관리자 *는 ODBC 2.x* 드라이버를 사용 하 여 작업 하는 경우 다음 단계를 수행 합니다.  
  
1.  *FSetPosError* 내부 드라이버 관리자 플래그를 TRUE로 초기화 합니다.  
  
2.  응용 프로그램이 **Sqlfetchscroll**을 호출 하면 드라이버 관리자는 *fSetPosError* 를 FALSE로 설정 합니다.  
  
3.  응용 프로그램에서 **SQLSetStmtAttr** 를 호출 하 여 SQL_ATTR_ROW_STATUS_PTR를 설정 하는 경우 드라이버 관리자는 *FSetPosError* equal totrue를 설정 합니다.  
  
4.  응용 프로그램이 **sqlsetpos**를 호출 하 고 *fSetPosError* 가 TRUE 인 경우 드라이버 SQL_ERROR 관리자는 SQLSTATE HY011 (지금 특성을 설정할 수 없음)을 사용 하 여 행 상태 포인터를 변경한 후 **sqlfetchscroll**을 호출 하기 전에 **sqlsetpos** 를 호출 하려고 했음을 나타낼 수 있습니다.

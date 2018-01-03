---
title: "상태 레코드 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3ca9f540f779894c06b22ced5e654381d86696ce
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="status-records"></a>상태 레코드
상태 레코드의 필드는 특정 오류 또는 경고 SQLSTATE, 원시 오류 번호, 진단 메시지, 열 번호 및 행 번호를 포함 하 여 드라이버 관리자, 드라이버 또는 데이터 원본에서 반환 하는 방법에 대 한 정보를 포함 합니다. 상태 레코드 함수 SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, sql_need_data가 또는 SQL_STILL_EXECUTING을 반환 하는 경우에 만들 수 있습니다. 상태 레코드의 필드 목록은 전체 참조는 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [상태 레코드의 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)

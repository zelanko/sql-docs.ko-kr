---
title: 상태 레코드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6ed360c39b87efe851bcbbb5c60762288ea1719
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114278"
---
# <a name="status-records"></a>상태 레코드
상태 레코드의 필드를 사용 하면 특정 오류 또는 SQLSTATE, 원시 오류 번호, 진단 메시지, 열 번호 및 행 번호를 포함 하 여 드라이버 관리자, 드라이버 또는 데이터 원본에 의해 반환 된 경고에 대 한 정보가 있습니다. 함수 SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA 또는 SQL_STILL_EXECUTING을 반환 하는 경우에 상태 레코드를 만들 수 있습니다. 상태 레코드의 필드의 전체 목록은 참조 합니다 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [상태 레코드의 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)

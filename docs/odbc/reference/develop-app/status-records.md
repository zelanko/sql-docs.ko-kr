---
description: 상태 레코드
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96d871814ac22e52eece4d6db7fff68fa2dacd48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482906"
---
# <a name="status-records"></a>상태 레코드
상태 레코드의 필드에는 SQLSTATE, 원시 오류 번호, 진단 메시지, 열 번호 및 행 번호를 포함 하 여 드라이버 관리자, 드라이버 또는 데이터 원본에서 반환 되는 특정 오류 또는 경고에 대 한 정보가 포함 됩니다. 함수에서 SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA 또는 SQL_STILL_EXECUTING를 반환 하는 경우에만 상태 레코드를 만들 수 있습니다. 상태 레코드의 전체 필드 목록은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명을 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [상태 레코드의 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)

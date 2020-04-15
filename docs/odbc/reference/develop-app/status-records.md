---
title: 상태 레코드 | 마이크로 소프트 문서
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
ms.openlocfilehash: 4afef16137404fcdfd3e1d328642f1d314829538
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301374"
---
# <a name="status-records"></a>상태 레코드
상태 레코드의 필드에는 SQLSTATE, 기본 오류 번호, 진단 메시지, 열 번호 및 행 번호를 포함하여 드라이버 관리자, 드라이버 또는 데이터 원본에서 반환된 특정 오류 또는 경고에 대한 정보가 포함됩니다. 상태 레코드는 함수가 SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA 또는 SQL_STILL_EXECUTING 반환하는 경우에만 만들 수 있습니다. 상태 레코드의 전체 필드 목록은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명을 참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [상태 레코드의 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [진단 메시지](../../../odbc/reference/develop-app/diagnostic-messages.md)

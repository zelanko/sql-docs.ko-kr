---
title: 드라이버 관리자의 역할 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee3d704ea43125c3cd912a4e67d90bf5d50c733e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304304"
---
# <a name="role-of-the-driver-manager"></a>드라이버 관리자의 역할
드라이버 관리자는 생성 된 상태 레코드를 반환 하는 마지막 순서를 결정 합니다. 특히 가장 높은 순위를 가지 며 먼저 반환 될 레코드를 결정 합니다. 드라이버는 생성 하는 상태 레코드의 순서를 지정 합니다. 드라이버 관리자와 드라이버 모두에서 상태 레코드를 게시 하는 경우 드라이버 관리자는 순서를 지정 해야 합니다. 자세한 내용은 [상태 레코드 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md)를 참조 하세요.  
  
 드라이버 관리자는 가능한 한 많은 오류 검사를 수행 합니다. 이렇게 하면 모든 드라이버가 동일한 오류를 확인 하지 않습니다. 예를 들어 함수 인수가 **SQLSetPos**의 *작업과* 같이 불연속 개수의 값을 허용 하는 경우 드라이버 관리자는 지정 된 값이 유효한 지 확인 합니다.  
  
 다음 섹션에서는 드라이버 관리자에 의해 확인 되는 조건 유형에 대해 설명 합니다. 완전 한 것은 아닙니다. 드라이버 관리자가 반환 하는 SQLSTATEs의 전체 목록은 각 함수의 "진단" 섹션을 참조 하세요. 드라이버 관리자에서 수행 하는 각 검사에 대 한 설명은 "(DM)" 문자로 시작 합니다. 또한 [부록 B: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)의 상태 전환 표를 참조 하세요. 괄호 안에 표시 된 오류는 드라이버 관리자에 의해 검색 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [인수 값 검사](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [상태 전환 검사](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [일반 오류 검사](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [드라이버 관리자 오류 및 경고 검사](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

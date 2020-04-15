---
title: 드라이버 관리자의 역할 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304304"
---
# <a name="role-of-the-driver-manager"></a>드라이버 관리자의 역할
드라이버 관리자는 생성되는 상태 레코드를 반환할 최종 순서를 결정합니다. 특히 순위가 가장 높은 레코드를 결정하고 먼저 반환해야 합니다. 드라이버는 생성되는 상태 레코드를 정렬할 책임이 있습니다. 드라이버 관리자와 드라이버 모두에 의해 상태 레코드가 게시되는 경우 드라이버 관리자는 상태 레코드를 정렬할 책임이 있습니다. 자세한 내용은 [상태 레코드 시퀀스를](../../../odbc/reference/develop-app/sequence-of-status-records.md)참조하십시오.  
  
 드라이버 관리자는 가능한 한 많은 오류 검사를 수행합니다. 이렇게 하면 모든 드라이버가 동일한 오류를 확인하지 못하게 됩니다. 예를 들어 함수 인수가 **SQLSetPos의** *작업과* 같은 개별 값 수를 허용하는 경우 드라이버 관리자는 지정된 값이 합법적인지 확인합니다.  
  
 다음 섹션에서는 드라이버 관리자가 검사하는 조건 유형을 설명합니다. 그들은 완전하게 의도되지 않습니다; 드라이버 관리자가 반환하는 SQLSTATEs의 전체 목록은 각 함수의 "진단" 섹션을 참조하십시오. 드라이버 관리자가 만든 각 검사에 대한 설명은 "(DM)"으로 시작합니다. 또한 [부록 B: ODBC 상태 전환 테이블의](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)상태 전환 테이블을 참조하십시오. 괄호 안에 표시된 오류는 드라이버 관리자에 의해 감지됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [인수 값 검사](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [상태 전환 검사](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [일반 오류 검사](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [드라이버 관리자 오류 및 경고 검사](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

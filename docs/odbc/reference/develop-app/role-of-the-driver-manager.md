---
title: 드라이버 관리자의 역할 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5985144c212988d8c35553f710f3edd40e6bfc1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="role-of-the-driver-manager"></a>드라이버 관리자의 역할
드라이버 관리자를 생성 하는 상태 레코드를 반환 하는 최종 순서를 결정 합니다. 특히 레코드 가장 높은 순위 개이고 먼저 반환 될 결정 합니다. 드라이버는 상태 레코드 생성 하는 순서를 지정 합니다. 상태 레코드 드라이버 관리자와 드라이버에 게시 하는 경우 드라이버 관리자는 순서를 지정 하는 일을 담당 합니다. 자세한 내용은 참조 [상태 레코드의 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md)합니다.  
  
 드라이버 관리자가 많은 오류를 검사 하면. 모든 드라이버를 저장이에서 동일한 오류를 확인 합니다. 예를 들어, 함수 인수와 같은 불연속 수의 값을 허용 하는 경우 *작업* 에 **SQLSetPos**, 지정된 된 값이 올바른 드라이버 관리자를 확인 합니다.  
  
 다음 섹션에서는 드라이버 관리자에서 확인 하는 조건 종류를 설명 합니다. 철저히;에 없습니다. 전체 목록은 드라이버 관리자 반환 SQLSTATEs, 각 함수의; "진단" 섹션을 참조 하십시오. 드라이버 관리자에서 만든 각 검사에 대 한 설명을 "DM ()."로 시작 또한의 상태 전환 테이블을 참조 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); 괄호 안에 표시 된 오류 드라이버 관리자에서 검색 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [인수 값 검사](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [상태 전환 검사](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [일반 오류 검사](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [드라이버 관리자 오류 및 경고 검사](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485cd951992ed427461e497c53d17a4f6db24a38
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626101"
---
# <a name="role-of-the-driver-manager"></a>드라이버 관리자의 역할
드라이버 관리자를 생성 하는 상태 레코드를 반환 하는 최종 순서를 결정 합니다. 특히 레코드 가장 높은 순위 있고 먼저 반환 될 결정 합니다. 드라이버는 생성 하는 상태 레코드를 정렬 하는 일을 담당 합니다. 상태 레코드 드라이버 관리자와 드라이버에서 게시 되는 경우 드라이버 관리자는 순서를 지정 하는 일을 담당 합니다. 자세한 내용은 [상태 레코드의 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md)합니다.  
  
 드라이버 관리자를 가져올 수 있는 많은 오류 검사를 수행 합니다. 이 동일한 오류에 대 한 확인에서 모든 드라이버를 저장 합니다. 예를 들어, 함수 인수는 불연속 값 개수를 같은 허용 *작업이* 에서 **SQLSetPos**, 드라이버 관리자는 지정 된 값을 법적 인지 확인 합니다.  
  
 다음 섹션에서는 드라이버 관리자에 의해 선택 조건의 유형을 설명 합니다. 확실히;에 적합 하지 드라이버 관리자 반환 된 Sqlstate의 전체 목록은 각 함수의; "진단" 섹션을 참조 하세요. 드라이버 관리자에 의해 수행 된 각 검사에 대 한 설명을 "(DM)."로 시작 상태 전환 테이블에서 참조 하세요 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); 괄호로 표시 된 오류 드라이버 관리자에 의해 검색 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [인수 값 검사](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [상태 전환 검사](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [일반 오류 검사](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [드라이버 관리자 오류 및 경고 검사](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

---
title: '3단계: SQL 문 작성 및 실행 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8322cf5e7b4a91bfc5f5f0204cfb25fa4bdad92
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306834"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>3단계: SQL 문 작성 및 실행
세 번째 단계는 다음 그림과 같이 SQL 문을 빌드하고 실행하는 것입니다. 이 단계를 수행하는 데 사용되는 방법은 엄청나게 다양할 수 있습니다. 응용 프로그램은 사용자에게 SQL 문을 입력하거나, 사용자 입력을 기반으로 SQL 문을 작성하거나, 하드 코딩된 SQL 문을 사용하도록 메시지를 표시할 수 있습니다. 자세한 내용은 [SQL 문 생성을](../../../odbc/reference/develop-app/constructing-sql-statements.md)참조하십시오.  
  
 ![SQL 문 작성 및 실행 방법](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 SQL 문에 매개 변수가 포함된 경우 응용 프로그램은 각 매개 변수에 대해 **SQLBindParameter를** 호출하여 응용 프로그램 변수에 바인딩합니다. 자세한 내용은 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
 SQL 문이 빌드되고 매개 변수가 바인딩되면 **SQLExecDirect**로 명령문이 실행됩니다. 명령문이 여러 번 실행되는 경우 **SQLPrepare를** 통해 준비하고 **SQLExecute**. 자세한 내용은 [명령문 실행](../../../odbc/reference/develop-app/executing-a-statement.md)을 참조하십시오.  
  
 또한 응용 프로그램은 SQL 문을 완전히 실행하는 것을 거부하고 대신 사용 가능한 열이나 테이블과 같은 카탈로그 정보가 포함된 결과 집합을 반환하는 함수를 호출할 수 있습니다. 자세한 내용은 [카탈로그 데이터 사용을](../../../odbc/reference/develop-app/uses-of-catalog-data.md)참조하십시오.  
  
 응용 프로그램의 다음 작업은 실행된 SQL 문의 유형에 따라 다릅니다.  
  
|SQL 문의 유형|계속하려면 다음을 진행하십시오.|  
|---------------------------|----------------|  
|**선택** 또는 카탈로그 기능|[4a단계: 결과 페치](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**업데이트,** **삭제**또는 **삽입**|[4b단계: 행 수 페치](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|기타 모든 SQL 문|3단계: SQL 문 빌드 및 실행(이 항목) 또는 [5단계: 트랜잭션 커밋](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|

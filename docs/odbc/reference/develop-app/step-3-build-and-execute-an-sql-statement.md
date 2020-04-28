---
title: '3 단계: SQL 문 작성 및 실행 | Microsoft Docs'
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306834"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>3단계: SQL 문 작성 및 실행
세 번째 단계는 다음 그림에 표시 된 것 처럼 SQL 문을 작성 하 고 실행 하는 것입니다. 이 단계를 수행 하는 데 사용 되는 방법은 크게 달라질 수 있습니다. 응용 프로그램은 사용자에 게 SQL 문을 입력 하거나, 사용자 입력을 기반으로 SQL 문을 작성 하거나, 하드 코드 된 SQL 문을 사용 하 라는 메시지를 표시할 수 있습니다. 자세한 내용은 [SQL 문 생성](../../../odbc/reference/develop-app/constructing-sql-statements.md)을 참조 하세요.  
  
 ![SQL 문 작성 및 실행 방법](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 SQL 문에 매개 변수가 포함 된 경우 응용 프로그램은 각 매개 변수에 대해 **SQLBindParameter** 를 호출 하 여 응용 프로그램 변수에 바인딩합니다. 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.  
  
 SQL 문을 작성 하 고 매개 변수를 바인딩한 후 **Sqlexecdirect**를 사용 하 여 문을 실행 합니다. 문이 여러 번 실행 될 경우 **Sqlprepare** 및 **sqlprepare**를 사용 하 여 실행할 수 있습니다. 자세한 내용은 [문 실행](../../../odbc/reference/develop-app/executing-a-statement.md)을 참조 하세요.  
  
 응용 프로그램은 SQL 문 실행을 완전히은 선형화 하 고 대신 함수를 호출 하 여 사용 가능한 열 또는 테이블과 같은 카탈로그 정보를 포함 하는 결과 집합을 반환 합니다. 자세한 내용은 [카탈로그 데이터 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)을 참조 하세요.  
  
 응용 프로그램의 다음 작업은 실행 되는 SQL 문 유형에 따라 달라 집니다.  
  
|SQL 문 유형|계속|  
|---------------------------|----------------|  
|**SELECT** 또는 catalog 함수|[4a단계: 결과 페치](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**업데이트**, **삭제**또는 **삽입**|[4b단계: 행 수 페치](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|다른 모든 SQL 문|3 단계: SQL 문 작성 및 실행 (이 항목) 또는 [5 단계: 트랜잭션 커밋](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|

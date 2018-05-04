---
title: '3 단계: 작성 하 고 SQL 문을 실행 하 | Microsoft Docs'
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
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f972fb5a0edfbbf492860e3421d5985d5e4edcc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>작성 하 고 SQL 문을 실행 하는 3 단계:
다음 그림에 나와 있는 것 처럼 작성 하 고 SQL 문을 실행 하는 세 번째 단계가입니다. 이 단계를 수행 하는 데 메서드는 매우 달라 집니다. 응용 프로그램 사용자 입력에 따라 SQL 문을 작성, SQL 문을 입력 하 라는 하거나 하드 코드 된 SQL 문을 사용 될 수 있습니다. 자세한 내용은 참조 [SQL 문을 생성](../../../odbc/reference/develop-app/constructing-sql-statements.md)합니다.  
  
 ![구축 하 고 SQL 문 실행을 보여 줍니다](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 SQL 문에 매개 변수가 있으면 응용 프로그램을 응용 프로그램 변수에 바인딩합니다 호출 하 여 **SQLBindParameter** 각 매개 변수에 대 한 합니다. 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.  
  
 문이 실행 되는 SQL 문이 작성 후 모든 매개 변수가 바인딩되지 **SQLExecDirect**합니다. 사용 하 여 준비 될 수는 문이 여러 번 실행 수, 하는 경우 **SQLPrepare** 있고와 실행 **SQLExecute**합니다. 자세한 내용은 참조 [문 실행](../../../odbc/reference/develop-app/executing-a-statement.md)합니다.  
  
 응용 프로그램도 함께 SQL 문을 실행 하지 말고 수도 있으며 대신 사용 가능한 열 또는 테이블과 같은 카탈로그 정보를 포함 하는 결과 집합을 반환 하는 함수를 호출할 수 있습니다. 자세한 내용은 참조 [카탈로그 데이터의 사용 하 여](../../../odbc/reference/develop-app/uses-of-catalog-data.md)합니다.  
  
 응용 프로그램의 다음 작업 실행 하는 SQL 문의 형식에 따라 달라 집니다.  
  
|SQL 문 유형|로 이동|  
|---------------------------|----------------|  
|**선택** 또는 카탈로그 함수|[4a단계: 결과 페치](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**업데이트**, **삭제**, 또는 **삽입**|[4b단계: 행 수 페치](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|다른 모든 SQL 문|3 단계: 작성 하 고 SQL 문 (이 항목)을 실행 또는 [5 단계: 트랜잭션 커밋](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|

---
title: '3 단계: 빌드 및 SQL 문을 실행할 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3427057e70ee27fe1108fde71c833f0c511836b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801371"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>3단계: SQL 문 작성 및 실행
다음 그림에 나와 있는 것 처럼 빌드는 SQL 문을 실행 하는 세 번째 단계가입니다. 이 단계를 수행 하는 데 사용 방법이 크게 달라 집니다. 응용 프로그램 사용자 입력을 기반으로 하는 SQL 문을 작성, SQL 문을 입력 하 라는 메시지가 수도 하드 코딩 된 SQL 문을 사용 합니다. 자세한 내용은 [SQL 문을 생성](../../../odbc/reference/develop-app/constructing-sql-statements.md)합니다.  
  
 ![빌드 및 SQL 문 실행을 보여 줍니다](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 SQL 문에 매개 변수가 있으면 응용 프로그램이 해당 응용 프로그램 변수에 바인딩합니다 호출 하 여 **SQLBindParameter** 각 매개 변수에 대 한 합니다. 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.  
  
 사용 하 여 문이 실행 된 SQL 문이 작성 후 모든 매개 변수에 바인딩되어 **SQLExecDirect**합니다. 문에 여러 번 실행할 수 있으면 사용 하 여 준비할 수 있습니다 **SQLPrepare** 실행 하 고 **SQLExecute**합니다. 자세한 내용은 [문을 실행](../../../odbc/reference/develop-app/executing-a-statement.md)합니다.  
  
 응용 프로그램도는 SQL 문 실행을 완전히 포기 하 고 사용 가능한 열 또는 테이블 등의 카탈로그 정보를 포함 하는 결과 집합을 반환 하도록 함수를 호출 하는 대신 수 있습니다. 자세한 내용은 [카탈로그 데이터의 사용](../../../odbc/reference/develop-app/uses-of-catalog-data.md)합니다.  
  
 응용 프로그램의 다음 작업 실행 된 SQL 문의 형식에 따라 달라 집니다.  
  
|SQL 문 유형|이동|  
|---------------------------|----------------|  
|**선택** 또는 카탈로그 함수|[4a단계: 결과 페치](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**업데이트**하십시오 **삭제할**, 또는 **삽입**|[4b단계: 행 수 페치](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|다른 모든 SQL 문|3 단계: 빌드 및 SQL 문 (이 항목)를 실행 하거나 [5 단계: 트랜잭션 커밋](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|

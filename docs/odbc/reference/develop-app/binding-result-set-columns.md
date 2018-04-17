---
title: 바인딩 결과 집합 열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 107a89aeca70d7b28958c475994e3c41f417fa26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="binding-result-set-columns"></a>바인딩 결과 집합 열
응용 프로그램은 모든 열이 없는 바인딩 포함 하 여 결과 선택에 따라 집합의 수가 많거나 적은 열으로 바인딩할 수 있습니다. 데이터 행을 인출할 때 드라이버는 응용 프로그램에 바인딩된 열에 대 한 데이터를 반환 합니다. 응용 프로그램 결과 집합의 모든 열으로 바인딩합니다 되는 여부는 응용 프로그램에 따라 달라 집니다. 예를 들어 일반적으로 보고서를 생성 하는 응용 프로그램을 고정된 형식으로에 이러한 응용 프로그램의 모든 보고서에 사용 되는 열을 포함 하는 결과 집합 및 바인딩할 만들고 모든 이러한 열에 대 한 데이터를 검색 합니다. 경우에 따라 데이터의 전체 화면을 표시 하는 응용 프로그램은 사용자에 게 표시할; 열을 허용 이러한 응용 프로그램 사용자 수를 있지만 바인딩 및 사용자가 선택한 열에 대해서만 데이터를 검색 하는 모든 열을 포함 한 결과 집합을 만듭니다.  
  
 호출 하 여 바인딩되지 않은 열에서 데이터를 검색할 수 **SQLGetData**합니다. 이 종종 단일 버퍼의 길이 초과 하 여 부분에서 검색 해야 하는 긴 데이터를 검색 하려면 일반적으로 호출 됩니다.  
  
 언제 든 지 행 인출 된 후에 열을 바인딩할 수 있습니다. 그러나 새 바인딩을 적용 하려면 하면 행이 인출; 때까지 되지 이미 인출 된 행에서 데이터에 적용 됩니다.  
  
 열은 호출 하 여 바인딩 해제 될 때까지 다른 변수 열을 바인딩할 때까지 한 변수는 열에 바인딩된 **SQLBindCol** 를호출하여모든열은바인딩해제될때까지해당변수의주소를null포인터로**SQLFreeStmt** 문을 해제 될 때까지 또는 SQL_UNBIND 옵션을 사용 합니다. 이러한 이유로 응용 프로그램으로 바인딩된 모든 바인딩된 변수로 계속 유효 확인 해야 합니다. 자세한 내용은 참조 [Allocating 및 버퍼 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)합니다.  
  
 열 바인딩 문 구조와 관련 된 정당한 정보 이기 때문에 어떤 순서로 든 설정할 수 있습니다. 결과 집합의 독립적인 수도 있습니다. 예를 들어, 응용 프로그램에서 다음 SQL 문을 생성 한 결과 집합의 열을 바인딩합니다.  
  
```  
SELECT * FROM Orders  
```  
  
 그런 다음 응용 프로그램에는 SQL 문을 실행 하는 경우  
  
```  
SELECT * FROM Lines  
```  
  
 동일한 문 핸들에서 첫 번째 결과 집합에 대 한 열 바인딩은 여전히 문의 구조에 저장 하는 바인딩 되입니다. 대부분의 경우에서 낮은 프로그래밍 관행 이며 피해 야 합니다. 대신, 응용 프로그램을 호출 해야 **SQLFreeStmt** 오래 된 모든 열을 바인딩 해제 하 고 다음 새 캠페인을 바인딩할 SQL_UNBIND 옵션과 함께 합니다.

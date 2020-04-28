---
title: 바인딩 결과 집합 열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 558ceb79d42d82477b70a028395de82cc023c170
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306364"
---
# <a name="binding-result-set-columns"></a>바인딩 결과 집합 열
응용 프로그램은 열을 전혀 바인딩하지 않는 것을 포함 하 여 선택 하는 것과 같이 결과 집합의 열을 여러 개 또는 여러 개 바인딩할 수 있습니다. 데이터 행을 인출할 때 드라이버는 바인딩된 열에 대 한 데이터를 응용 프로그램에 반환 합니다. 응용 프로그램이 결과 집합의 모든 열을 바인딩하는 지 여부는 응용 프로그램에 따라 달라 집니다. 예를 들어 보고서를 생성 하는 응용 프로그램에는 일반적으로 고정 된 형식이 있습니다. 이러한 응용 프로그램은 보고서에 사용 된 모든 열을 포함 하는 결과 집합을 만든 다음 이러한 모든 열에 대 한 데이터를 바인딩하고 검색 합니다. 화면에 전체 데이터를 표시 하는 응용 프로그램에서는 사용자가 표시할 열을 결정할 수 있습니다. 이러한 응용 프로그램은 사용자가 원하는 모든 열을 포함 하는 결과 집합을 만들지만 사용자가 선택한 열에 대해서만 데이터를 바인딩하고 검색할 수 있습니다.  
  
 **SQLGetData**를 호출 하 여 바인딩되지 않은 열에서 데이터를 검색할 수 있습니다. 이는 대개 단일 버퍼의 길이를 초과 하는 long 데이터를 검색 하기 위해 호출 되며 파트에서 검색 해야 합니다.  
  
 행이 인출 된 후에도 언제 든 지 열을 바인딩할 수 있습니다. 그러나 다음에 행을 반입할 때까지 새 바인딩이 적용 되지 않습니다. 이미 인출 된 행의 데이터에는 적용 되지 않습니다.  
  
 변수는 다른 변수가 열에 바인딩될 때까지 다른 변수가 열에 바인딩될 때까지 **SQLBindCol** 를 호출 하 여 모든 열이 SQL_UNBIND 옵션으로 **SQLFreeStmt** 를 호출 하 여 바인딩 해제 될 때까지 또는 문이 해제 될 때까지 해당 열이 바인딩 해제 될 때까지 열에 바인딩되어 있습니다. 이러한 이유로 응용 프로그램은 바인딩된 모든 변수가 바인딩된 경우에도 유효한 상태로 유지 되도록 해야 합니다. 자세한 내용은 [버퍼 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)를 참조 하세요.  
  
 열 바인딩은 문 구조와 관련 된 정보 일 뿐 이므로 순서에 관계 없이 설정할 수 있습니다. 또한 결과 집합에 독립적입니다. 예를 들어 응용 프로그램이 다음 SQL 문에 의해 생성 된 결과 집합의 열을 바인딩하는 경우를 가정 합니다.  
  
```  
SELECT * FROM Orders  
```  
  
 응용 프로그램에서 SQL 문을 실행 하는 경우  
  
```  
SELECT * FROM Lines  
```  
  
 동일한 문 핸들에서 첫 번째 결과 집합에 대 한 열 바인딩은 문 구조에 저장 된 바인딩 이므로 여전히 적용 됩니다. 대부분의 경우이는 잘못 된 프로그래밍 습관 이므로 피해 야 합니다. 대신 응용 프로그램은 SQL_UNBIND 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하 여 모든 이전 열을 바인딩 해제 한 다음 새 열을 바인딩해야 합니다.

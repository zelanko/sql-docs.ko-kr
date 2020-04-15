---
title: 바인딩 결과 세트 열 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306364"
---
# <a name="binding-result-set-columns"></a>바인딩 결과 집합 열
응용 프로그램은 열 바인딩을 포함하여 결과 집합의 열수를 선택함에 따라 바인딩할 수 있습니다. 데이터 행을 가져오면 드라이버는 바인딩된 열에 대한 데이터를 응용 프로그램에 반환합니다. 응용 프로그램이 결과 집합의 모든 열을 바인딩하는지 여부는 응용 프로그램에 따라 다릅니다. 예를 들어 보고서를 생성하는 응용 프로그램에는 일반적으로 고정 형식이 있습니다. 이러한 응용 프로그램은 보고서에 사용된 모든 열을 포함하는 결과 집합을 만든 다음 이러한 모든 열에 대한 데이터를 바인딩하고 검색합니다. 데이터가 가득 찬 화면을 표시하는 응용 프로그램은 때때로 사용자가 표시할 열을 결정할 수 있습니다. 이러한 응용 프로그램은 사용자가 원하는 모든 열을 포함하는 결과 집합을 만들지만 사용자가 선택한 열에 대해서만 데이터를 바인딩하고 검색합니다.  
  
 **SQLGetData**를 호출하여 언바운드 열에서 데이터를 검색할 수 있습니다. 일반적으로 긴 데이터를 검색하기 위해 호출되며, 이는 종종 단일 버퍼의 길이를 초과하며 부분적으로 검색해야 합니다.  
  
 행을 가져온 후에도 열은 언제든지 바인딩할 수 있습니다. 그러나 새 바인딩은 다음에 행을 가져올 때까지 적용되지 않습니다. 이미 가져온 행의 데이터에는 적용되지 않습니다.  
  
 다른 변수가 열에 바인딩될 때까지, 모든 열이 SQL_UNBIND 옵션으로 **SQLFreeStmt를** 호출하여 바인딩되지 않을 때까지 또는 문이 해제될 때까지 모든 열이 변수의 주소로 null 포인터를 **호출하여** 바인딩되지 않을 때까지 변수는 열에 바인딩됩니다. 따라서 응용 프로그램은 바인딩된 모든 변수가 바인딩된 동안 유효한 상태로 유지되어야 합니다. 자세한 내용은 [버퍼 할당 및 해제 를](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)참조하십시오.  
  
 열 바인딩은 문 구조와 연결된 정보일 뿐이므로 순서에 따라 설정할 수 있습니다. 또한 결과 집합과 독립적입니다. 예를 들어 응용 프로그램이 다음 SQL 문에 의해 생성된 결과 집합의 열을 바인딩한다고 가정합니다.  
  
```  
SELECT * FROM Orders  
```  
  
 응용 프로그램이 SQL 문을 실행하는 경우  
  
```  
SELECT * FROM Lines  
```  
  
 동일한 문 핸들에서 첫 번째 결과 집합에 대한 열 바인딩은 문 구조에 저장된 바인딩이기 때문에 여전히 유효합니다. 대부분의 경우 이는 프로그래밍 관행이 좋지 않으며 피해야 합니다. 대신 응용 프로그램은 모든 이전 열을 바인딩 해제한 다음 새 열을 바인딩하는 SQL_UNBIND 옵션을 사용하여 **SQLFreeStmt를** 호출해야 합니다.

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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92f317d72410a5dff56652dd9de1e3b2ba5c9cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47725911"
---
# <a name="binding-result-set-columns"></a>바인딩 결과 집합 열
응용 프로그램은 결과 집합 선택한 모든 열이 없는 바인딩 등의 많거나 적은 열으로 바인딩할 수 있습니다. 데이터 행을 인출할 때 드라이버 응용 프로그램에 바인딩된 열에 대 한 데이터를 반환 합니다. 응용 프로그램 결과 집합의 모든 열으로 바인딩합니다 되는 여부는 응용 프로그램에 따라 달라 집니다. 예를 들어, 일반적으로 보고서를 생성 하는 응용 프로그램 형식이 고정; 이러한 응용 프로그램의 모든 보고서에 사용 되는 열을 포함 하는 결과 집합을 바인딩하고 만들고 이러한 열의 모든 데이터를 검색 합니다. 경우에 따라 데이터의 전체 화면을 표시 하는 응용 프로그램에는 사용자가; 표시할 열을 결정 하도록 허용 이러한 응용 프로그램 결과 사용자 수를 하지만 바인딩 및 사용자가 선택한 열에 대해서만 데이터를 검색 하는 모든 열이 포함 된 집합을 만듭니다.  
  
 호출 하 여 바인딩되지 않은 열에서 데이터를 검색할 수 있습니다 **SQLGetData**합니다. 이 종종 단일 버퍼의 길이 초과 하 여 부분에서 검색 해야 하는 긴 데이터를 검색 하려면 일반적으로 호출 됩니다.  
  
 언제 든 지 행 인출 된 후에 열을 바인딩할 수 있습니다. 그러나 새 바인딩을 적용 하려면 행이 인출; 전 까지는 하지 이미 인출 된 행의 데이터에 적용 됩니다.  
  
 변수까지 열에 바인딩된 열은 호출 하 여 바인딩 해제 될 때까지 다른 변수 열에 바인딩된 **SQLBindCol** 를호출하여모든열은바인딩해제될때까지변수주소로null포인터를사용하여**SQLFreeStmt** SQL_UNBIND 옵션과 또는 문을 해제 될 때까지 합니다. 이러한 이유로 응용 프로그램으로 바인딩된 모든 바인딩된 변수로 유효 있는지 확인 해야 합니다. 자세한 내용은 [Allocating 및 버퍼 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)합니다.  
  
 열 바인딩 문 구조와 관련 된 정보만 이기 때문에 순서에 관계 없이 설정할 수 있습니다. 결과 집합의 독립적인 수도 있습니다. 예를 들어 응용 프로그램이 다음 SQL 문으로 생성 된 결과 집합의 열을 바인딩하는 것으로 가정 합니다.  
  
```  
SELECT * FROM Orders  
```  
  
 그런 다음 응용 프로그램에는 SQL 문을 실행 하는 경우  
  
```  
SELECT * FROM Lines  
```  
  
 동일한 문 핸들에 대해 첫 번째 결과 집합의 열 바인딩이 아직 효과 문의 구조에 저장 된 바인딩을 이기 때문입니다. 대부분의 경우에서 잘못 된 프로그래밍 방법 이며 하지 않아야 합니다. 응용 프로그램 대신 호출 해야 **SQLFreeStmt** 이전 모든 열을 바인딩 해제 하 고 새로 바인딩하고 SQL_UNBIND 옵션과 함께 합니다.

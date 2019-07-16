---
title: UPDATE, DELETE 및 INSERT 문의 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2a2787be1bf44e1f214d396444a73b938acf7ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942833"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE, DELETE 및 INSERT 문
SQL 기반 응용 프로그램 실행 하 여 테이블에 변경 내용을 확인 합니다 **업데이트**, **삭제**, 및 **삽입** 문입니다. 이러한 문은 SQL 최소 문법 규칙 수준은의 일부 이며 모든 드라이버 및 데이터 원본에서 지원 되어야 합니다.  
  
 이러한 문의 구문은 다음과 같습니다.  
  
 **UPDATE** _table-name_  
  
 **설정할** _열 식별자_ **=** {*식* &#124; **NULL**}  
  
 [**하십시오** _열 식별자_ **=** {*식* &#124; **NULL**}]...  
  
 [**WHERE** _search-condition_]  
  
 **DELETE FROM** _table-name_[**WHERE** _search-condition_]  
  
 **INSERT INTO** _테이블 이름_[ **(** _열 식별자_ [**하십시오** _열 식별자_]... **)** ]  
  
 {*쿼리 사양* &#124; **값 (** _삽입 값_ [**하십시오** _삽입 값_]... **)** }  
  
 *쿼리 사양* 요소는 및 코어 및 확장 SQL 문법의 경우에 유효 합니다 *식* 및 *검색 조건을* 요소 정하여 코어 및 확장 SQL 문법에 복합 형식입니다.  
  
 같은 다른 SQL 문에도 **업데이트**를 **삭제**, 및 **삽입** 문을 많습니다 매개 변수를 사용할 때 효율적입니다. 예를 들어, 다음 문은 준비 하 고 반복적으로 실행할 수 Orders 테이블의 여러 행을 삽입 합니다.  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 매개 변수 값 배열을 전달 하 여 이러한 효율성을 늘릴 수 있습니다. 문 매개 변수 및 매개 변수 값의 배열에 대 한 자세한 내용은 참조 하세요. [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.

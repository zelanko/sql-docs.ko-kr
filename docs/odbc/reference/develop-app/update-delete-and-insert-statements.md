---
title: 문의 업데이트, 삭제 및 삽입 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f12682a5d012d6981afce0085e9c920ed2f2ffbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284263"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE, DELETE 및 INSERT 문
SQL 기반 응용 프로그램은 **UPDATE,** **DELETE**및 **INSERT** 문을 실행하여 테이블을 변경합니다. 이러한 문은 최소 SQL 문법 준수 수준의 일부이며 모든 드라이버 및 데이터 원본에서 지원해야 합니다.  
  
 이러한 명령문의 구문은 다음과 있습니다.  
  
 **테이블** _이름_ 업데이트  
  
 **SET** _열 식별자_ **=** {*NULL}* &#124; 식 **NULL**  
  
 ▲ **,** _열 식별자_ **=** {*식* &#124; **NULL**}]...  
  
 [**어디** _검색 조건_]  
  
 _테이블 이름에서_ **삭제** [**여기서** _검색 조건]_  
  
 **테이블** _이름에_삽입 [**[(열** _식별자_ [**,** _열 식별자]..._ **)**]  
  
 {*쿼리 사양* &#124; 값 **(삽입** _값_ [**,** 삽입 _값]..._ **)**}  
  
 *쿼리 사양* 요소는 코어 및 확장 SQL 문법에서만 유효하며 *표현식* 및 *검색 조건* 요소는 코어 및 확장 SQL 문법에서 더 복잡해집니다.  
  
 다른 SQL 문과 마찬가지로 **UPDATE**, **DELETE**및 **INSERT** 문은 매개 변수를 사용할 때 더 효율적입니다. 예를 들어 Orders 테이블에 여러 행을 삽입하기 위해 다음 문을 준비하고 반복적으로 실행할 수 있습니다.  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 이러한 효율성은 매개 변수 값의 배열을 전달하여 증가할 수 있습니다. 문 매개 변수 및 매개 변수 값의 배열에 대한 자세한 내용은 [문 매개 변수 를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.

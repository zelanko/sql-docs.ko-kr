---
title: UPDATE, DELETE 및 INSERT 문 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284263"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE, DELETE 및 INSERT 문
SQL 기반 응용 프로그램은 **UPDATE**, **DELETE**및 **INSERT** 문을 실행 하 여 테이블을 변경 합니다. 이러한 문은 최소 SQL 문법 규칙 수준의 일부 이며 모든 드라이버 및 데이터 원본에서 지원 되어야 합니다.  
  
 이러한 문의 구문은 다음과 같습니다.  
  
 **UPDATE** _테이블 이름_ 업데이트  
  
 **SET** _열 식별자_ **=** {*expression* &#124; **NULL**} 설정  
  
 [**,** _열 식별자_ **=** {*expression* &#124; **NULL**}] ...  
  
 [**WHERE** _검색 조건_]  
  
 _테이블 이름_ **에서 삭제** **[** _검색 조건_]  
  
 테이블 **에 삽입** _-이름_[**(** _열 식별자_ [**,** _열 식별자_] ... **)**]  
  
 {*쿼리 사양* &#124; **값 (** _값 삽입_ [**,** _값 삽입_] ... **)**}  
  
 *쿼리 사양* 요소는 핵심 및 확장 된 sql 문법 에서만 유효 하며, *식* 및 *검색 조건* 요소가 핵심 및 확장 된 sql 문법에서 더 복잡 하 게 됩니다.  
  
 다른 SQL 문 처럼 **UPDATE**, **DELETE**및 **INSERT** 문은 매개 변수를 사용 하는 경우에 더 효율적입니다. 예를 들어 다음 문을 준비 하 고 반복적으로 실행 하 여 Orders 테이블에 여러 행을 삽입할 수 있습니다.  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 매개 변수 값의 배열을 전달 하 여 이러한 효율성을 높일 수 있습니다. 문 매개 변수 및 매개 변수 값 배열에 대 한 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.

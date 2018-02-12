---
title: "UPDATE, DELETE 및 INSERT 문을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 592d135ccf66f8a9fde2cc064a51dc25617cf127
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="update-delete-and-insert-statements"></a>UPDATE, DELETE 및 INSERT 문
SQL 기반 응용 프로그램을 실행 하 여 테이블에 변경 내용을 확인는 **업데이트**, **삭제**, 및 **삽입** 문. 이러한 문은 최소 SQL 문법의 규칙 수준과의 일부 이며 모든 드라이버 및 데이터 원본에서 지원 되어야 합니다.  
  
 이러한 문의 구문은 다음과 같습니다.  
  
 **UPDATE**  *table-name*  
  
 **SET** *column-identifier* **=** {*expression* &#124; **NULL**}  
  
 [**,** *column-identifier* **=** {*expression* &#124; **NULL**}]...  
  
 [**WHERE** *search-condition*]  
  
 **DELETE FROM** *table-name*[**WHERE** *search-condition*]  
  
 **INSERT INTO** *table-name*[**(***column-identifier* [**,** *column-identifier*]...**)**]  
  
 {*쿼리 사양* &#124;  **값 (* * * 삽입 값* [* *,** *삽입 값*]... **)**}  
  
 *쿼리 사양* 요소는 핵심 및 확장 SQL 문법을 지정 하 고 있는 경우에 유효는 *식* 및 *검색 조건* 요소 정하여 핵심 및 확장 SQL 문법에 복잡 한 합니다.  
  
 다른 SQL 문의 경우 처럼 **업데이트**, **삭제**, 및 **삽입** 문을 더 효율적인 매개 변수를 사용할 때. 예를 들어 다음 문은 준비 및 반복적으로 실행 되어 Orders 테이블에서 여러 행을 삽입할 수 있습니다.  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 매개 변수 값 배열을 전달 하 여 이러한 효율성을 늘릴 수 있습니다. 문 매개 변수 및 매개 변수 값의 배열에 대 한 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.

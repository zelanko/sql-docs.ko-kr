---
title: "UPDATE, DELETE 및 INSERT 문을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b150288c113b1aebf92abedbd6f7eabd0b4b7d24
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="update-delete-and-insert-statements"></a>UPDATE, DELETE 및 INSERT 문
SQL 기반 응용 프로그램을 실행 하 여 테이블에 변경 내용을 확인는 **업데이트**, **삭제**, 및 **삽입** 문. 이러한 문은 최소 SQL 문법의 규칙 수준과의 일부 이며 모든 드라이버 및 데이터 원본에서 지원 되어야 합니다.  
  
 이러한 문의 구문은 다음과 같습니다.  
  
 **업데이트***테이블 이름*   
  
 **설정** *열 식별자*  **=**  {*식* &#124; **NULL**}  
  
 [**,** *열 식별자*  **=**  {*식* &#124; **NULL**}]...  
  
 [**여기서** *검색 조건*]  
  
 **DELETE FROM** *테이블 이름*[**여기서** *검색 조건*]  
  
 **INSERT INTO** *테이블 이름*[**(***열 식별자* [**,** *열 식별자*] ... **)**]  
  
 {*쿼리 사양* &#124; **값 (***삽입 값* [**,** *삽입 값*]... **)**}  
  
 *쿼리 사양* 요소는 핵심 및 확장 SQL 문법을 지정 하 고 있는 경우에 유효는 *식* 및 *검색 조건* 요소 정하여 핵심 및 확장 SQL 문법에 복잡 한 합니다.  
  
 다른 SQL 문의 경우 처럼 **업데이트**, **삭제**, 및 **삽입** 문을 더 효율적인 매개 변수를 사용할 때. 예를 들어 다음 문은 준비 및 반복적으로 실행 되어 Orders 테이블에서 여러 행을 삽입할 수 있습니다.  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 매개 변수 값 배열을 전달 하 여 이러한 효율성을 늘릴 수 있습니다. 문 매개 변수 및 매개 변수 값의 배열에 대 한 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.


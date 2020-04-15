---
title: LIKE 조건자 탈출 문자 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e4f04b12911145eede3354532736cb92f1ae413
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306154"
---
# <a name="like-predicate-escape-character"></a>LIKE 조건자 이스케이프 문자
**LIKE** 조건자에서 백분율 기호(%) 모든 문자의 0 이상과 일치하고 밑줄(_)은 한 문자와 일치합니다. **LIKE** 조건자에서 실제 백분율 기호 또는 밑줄과 일치하려면 이스케이프 문자가 백분율 기호 또는 밑줄 앞에 와야 합니다. **LIKE** 조건자 이스케이프 문자를 정의하는 이스케이프 시퀀스는 다음과 같습니다.  
  
 **{이스케이프 '** *이스케이프 문자* **'}**  
  
 *여기서 이스케이프 문자는* 데이터 원본에서 지원하는 모든 문자입니다.  
  
 LIKE 이스케이프 시퀀스에 대한 자세한 내용은 부록 C: SQL 문법의 [LIKE 이스케이프 시퀀스를](../../../odbc/reference/appendixes/like-escape-sequence.md) 참조하십시오.  
  
 예를 들어 다음 SQL 문은 "%AAA"로 시작하는 동일한 고객 이름 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용합니다. 두 번째 문은 Microsoft® Access에 대한 기본 구문을 사용하며 상호 운용할 수 없습니다. 각 **LIKE** 조건자의 두 번째 백분율 문자는 모든 문자의 0 이상과 일치하는 와일드카드 문자입니다.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 **LIKE** 조건자 이스케이프 문자가 데이터 원본에서 지원되는지 여부를 확인하기 위해 응용 프로그램은 SQL_LIKE_ESCAPE_CLAUSE 옵션을 사용하여 **SQLGetInfo를** 호출합니다.

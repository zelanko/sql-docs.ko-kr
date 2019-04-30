---
title: LIKE 조건자 이스케이프 문자 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30547551cc1793622eaa981c07bbc002d07a094d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312916"
---
# <a name="like-predicate-escape-character"></a>LIKE 조건자 이스케이프 문자
에 **같은** 조건자 백분율 기호 (%) 일치 항목 0 개 이상의 문자 및 밑줄 (_)에 하나의 문자와 일치 합니다. 실제 백분율 기호를 검색 하거나 검색할에서 밑줄을 **같은** 조건자에 이스케이프 문자가 앞에 나와야 합니다 백분율 기호 또는 밑줄. 정의 하는 이스케이프 시퀀스를 **같은** 조건자 이스케이프 문자는:  
  
 **{escape '** *escape-character* **'}**  
  
 여기서 *이스케이프 문자* 는 데이터 원본에서 지 원하는 모든 문자입니다.  
  
 자세한 내용은 같은 이스케이프 시퀀스를 참조 하세요 [이스케이프 시퀀스와 같은](../../../odbc/reference/appendixes/like-escape-sequence.md) 부록 c: SQL 문법입니다.  
  
 예를 들어, 다음 SQL 문을 이름이 "%AAA" 문자로 시작 하는 고객의 동일한 결과 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스가 구문을 사용 합니다. 두 번째 문은 Microsoft® Access에 대 한 기본 구문을 사용 하 고 상호 운용은 불가능 합니다. 두 번째 % 각 문자는 **같은** 조건자는 0 개 이상의 문자와 일치 하는 와일드 카드 문자입니다.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 결정할 여부를 합니다 **와 같은** 조건자 이스케이프 문자는 데이터 원본에서 지 원하는, 응용 프로그램이 호출 **SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 옵션을 사용 하 여 합니다.

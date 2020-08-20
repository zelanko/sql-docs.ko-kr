---
description: LIKE 조건자 이스케이프 문자
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5304068e21dd6faf0e737a94add0cce177c4dabc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476555"
---
# <a name="like-predicate-escape-character"></a>LIKE 조건자 이스케이프 문자
**LIKE** 조건자에서 백분율 기호 (%) 는 임의의 문자를 0 개 이상 찾지만 밑줄 (_)은 임의의 문자 하나에 대응 합니다. **LIKE** 조건자에서 실제 백분율 기호 또는 밑줄을 일치 시키려면 이스케이프 문자가 백분율 부호 또는 밑줄 앞에와 야 합니다. **LIKE** 조건자 이스케이프 문자를 정의 하는 이스케이프 시퀀스는 다음과 같습니다.  
  
 **{escape '** *이스케이프 문자* **'}**  
  
 여기서 *이스케이프 문자* 는 데이터 원본에서 지 원하는 모든 문자입니다.  
  
 LIKE 이스케이프 시퀀스에 대 한 자세한 내용은 부록 C: SQL 문법의 [Like 이스케이프 시퀀스](../../../odbc/reference/appendixes/like-escape-sequence.md) 를 참조 하세요.  
  
 예를 들어 다음 SQL 문은 "% AAA" 문자로 시작 하는 동일한 고객 이름 결과 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용 합니다. 두 번째 문은 Microsoft® Access의 기본 구문을 사용 하며 상호 운용할 수 없습니다. 각 **LIKE** 조건자에서 두 번째 백분율 문자는 0 개 이상의 문자와 일치 하는 와일드 카드 문자입니다.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 **LIKE** 조건자 이스케이프 문자가 데이터 소스에서 지원 되는지 여부를 확인 하기 위해 응용 프로그램은 SQL_LIKE_ESCAPE_CLAUSE 옵션으로 **SQLGetInfo** 를 호출 합니다.

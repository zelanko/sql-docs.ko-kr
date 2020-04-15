---
title: 리터럴 접두사 및 접미사 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d52ca54c329353e3d9dc67ca35d89b2d28cedf74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287985"
---
# <a name="literal-prefixes-and-suffixes"></a>리터럴 접두사 및 접미사
SQL 문에서 *리터럴은* 실제 데이터 값의 문자 표현입니다. 예를 들어 다음 명령문에서 ABC, FFFF 및 10은 리터럴입니다.  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 일부 데이터 형식의 리터럴에는 특수 접두사와 접미사가 필요합니다. 앞의 예제에서 문자 리터럴(ABC)은 접두사와 접미사 모두로 단일 따옴표(')를 필요로 하고, 이진 리터럴(FFFF)은 문자 0을 접두사로 필요로 하며 정수 리터럴(10)은 접두사 나 접미사가 필요하지 않습니다.  
  
 날짜, 시간 및 타임스탬프를 제외한 모든 데이터 형식의 경우 상호 운용 가능한 응용 프로그램은 LITERAL_PREFIX 반환되는 값과 **SQLGetTypeInfo에서**만든 결과 집합의 LITERAL_SUFFIX 열을 사용해야 합니다. 날짜, 시간, 타임스탬프 및 날짜 시간 간격 리터럴의 경우 상호 운용 가능한 응용 프로그램은 이전 섹션에서 설명한 이스케이프 시퀀스를 사용해야 합니다.

---
title: "리터럴 접두사와 접미사로 | Microsoft Docs"
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff05f946dee8f6034d04c5d719ada475255ba643
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="literal-prefixes-and-suffixes"></a>리터럴 접두사 및 접미사
SQL 문에서 *리터럴* 실제 데이터 값의 문자 표시 됩니다. 예를 들어 다음 문에서 ABC, FFFF, 및 10은 리터럴:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 일부 데이터 형식의 리터럴 특수 접두사와 접미사에 필요합니다. 앞의 예제에서 문자 리터럴을 (ABC) 접두사와 접미사를 모두 작은따옴표 (')를 사용 하려면, 이진 리터럴 (FFFF)는 접두사와 정수 리터럴 (10)로 0 x 접두사가 필요 하지 않거나 접미사 문자가 필요 함.  
  
 날짜, 시간 및 타임 스탬프를 제외한 모든 데이터 형식에 대 한 상호 운용 가능한 응용 프로그램에서 만든 결과 집합의 LITERAL_PREFIX 및 LITERAL_SUFFIX 열에 반환 된 값을 사용 해야 **SQLGetTypeInfo**합니다. 날짜, 시간, 타임 스탬프 및 날짜/시간 간격 리터럴 상호 운용 가능한 응용 프로그램 이전 섹션에 설명 된 이스케이프 시퀀스 사용 해야 합니다.


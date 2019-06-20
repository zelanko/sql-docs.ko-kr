---
title: 리터럴 접두사 및 접미사 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4eabc3e0c354e02ad8df790d896dc43ae49c9bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313006"
---
# <a name="literal-prefixes-and-suffixes"></a>리터럴 접두사 및 접미사
SQL 문에서 *리터럴* 실제 데이터 값의 문자 표시 됩니다. 예를 들어 다음 문에서 ABC, FFFF 및 10에 리터럴:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 일부 데이터 형식에 대 한 리터럴을 특수 한 접두사 및 접미사 필요합니다. 앞의 예제에서 문자 리터럴 (ABC) 접두사 및 접미사를 모두 작은따옴표 (') 필요, 이진 리터럴 (FFFF) 접두사 및 정수 리터럴 (10)로 0 x 접두사가 필요한 하지 않거나 접미사 문자 필요 합니다.  
  
 날짜, 시간 및 타임 스탬프를 제외한 모든 데이터 형식에 대해 상호 운용 가능한 응용 프로그램 LITERAL_PREFIX 및 LITERAL_SUFFIX 만들어 결과 집합 열에 반환 되는 값을 사용 해야 **SQLGetTypeInfo**합니다. 날짜, 시간, 타임 스탬프 및 날짜/시간 간격 리터럴에 대 한 상호 운용 가능한 응용 프로그램에는 이전 섹션에서 설명 하는 이스케이프 시퀀스를 사용 해야 합니다.

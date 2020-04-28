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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d52ca54c329353e3d9dc67ca35d89b2d28cedf74
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287985"
---
# <a name="literal-prefixes-and-suffixes"></a>리터럴 접두사 및 접미사
SQL 문에서 *리터럴은* 실제 데이터 값의 문자 표현입니다. 예를 들어 다음 문에서 ABC, FFFF 및 10은 리터럴입니다.  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 일부 데이터 형식에 대 한 리터럴에는 특수 접두사 및 접미사가 필요 합니다. 앞의 예제에서 문자 리터럴 (ABC)에는 접두사와 접미사로 작은따옴표 (')가 필요 하 고, 이진 리터럴 (FFFF)에는 0x 문자를 접두사로 사용 해야 하 고, 정수 리터럴 (10)에는 접두사 또는 접미사가 필요 하지 않습니다.  
  
 날짜, 시간 및 타임 스탬프를 제외한 모든 데이터 형식에 대해 상호 운용 가능한 응용 프로그램은 **SQLGetTypeInfo**에서 생성 된 결과 집합의 LITERAL_SUFFIX 열 및 LITERAL_PREFIX에 반환 된 값을 사용 해야 합니다. 날짜, 시간, 타임 스탬프 및 날짜/시간 간격 리터럴의 경우, 상호 운용 가능한 응용 프로그램은 이전 섹션에서 설명한 이스케이프 시퀀스를 사용 해야 합니다.

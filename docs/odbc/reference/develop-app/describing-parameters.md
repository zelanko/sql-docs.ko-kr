---
title: 매개 변수 설명 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4d9284294707da0a469bf75ff9812ad5f7855bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305944"
---
# <a name="describing-parameters"></a>매개 변수 설명
**SQLBindParameter** 매개 변수를 설명 하는 인수: 해당 SQL 형식, 정밀도 및 배율. 드라이버는 이 정보 또는 *메타데이터를* 사용하여 매개 변수 값을 데이터 원본에 필요한 유형으로 변환합니다. 언뜻 보기에 드라이버가 응용 프로그램보다 매개 변수 메타데이터를 알 수 있는 더 나은 위치에 있는 것처럼 보일 수 있습니다. 결국 드라이버는 결과 집합 열의 메타데이터를 쉽게 검색할 수 있습니다. 알고 보니, 이것은 사실이 아닙니다. 첫째, 대부분의 데이터 원본은 드라이버가 매개 변수 메타데이터를 검색할 수 있는 방법을 제공하지 않습니다. 둘째, 대부분의 응용 프로그램은 이미 메타데이터를 알고 있습니다.  
  
 SQL 문이 응용 프로그램에서 하드 코딩된 경우 응용 프로그램 작성기는 이미 각 매개 변수의 형식을 알고 있습니다. SQL 문은 런타임에 응용 프로그램에 의해 생성되는 경우 응용 프로그램은 문을 작성할 때 메타데이터를 확인할 수 있습니다. 예를 들어 응용 프로그램이 절을 생성하는 경우  
  
```  
WHERE OrderID = ?  
```  
  
 OrderID 열에 대해 **SQLColumns를** 호출할 수 있습니다.  
  
 응용 프로그램이 매개 변수 메타데이터를 쉽게 확인할 수 없는 유일한 상황은 사용자가 매개 변수로 된 문을 입력할 때입니다. 이 경우 응용 프로그램은 **SQLPrepare를** 호출하여 문을 준비하고, **SQLNumParams는** 매개 변수 수를 결정하고, **SQLDescribeParam은** 각 매개 변수를 설명합니다. 그러나 앞서 설명한 것처럼 대부분의 데이터 원본은 드라이버가 매개 변수 메타데이터를 검색할 수 있는 방법을 제공하지 않으므로 **SQLDescribeParam은** 널리 지원되지 않습니다.

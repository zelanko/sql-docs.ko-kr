---
title: 매개 변수 설명 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d32e5212ba1ba28262d871498f2974485d38233
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68040026"
---
# <a name="describing-parameters"></a>매개 변수 설명
**SQLBindParameter** 에는 매개 변수를 설명 하는 인수 (SQL 유형, 전체 자릿수 및 소수 자릿수)가 있습니다. 드라이버는이 정보 또는 *메타 데이터를* 사용 하 여 매개 변수 값을 데이터 원본에 필요한 형식으로 변환 합니다. 먼저 드라이버가 응용 프로그램 보다 매개 변수 메타 데이터를 알 수 있는 위치에 있는 것 처럼 보일 수 있습니다. 그 후 드라이버는 결과 집합 열에 대 한 메타 데이터를 쉽게 검색할 수 있습니다. 이 경우에는 그렇지 않습니다. 첫째, 대부분의 데이터 원본은 드라이버에서 매개 변수 메타 데이터를 검색할 수 있는 방법을 제공 하지 않습니다. 둘째, 대부분의 응용 프로그램은 메타 데이터를 이미 알고 있습니다.  
  
 응용 프로그램에서 SQL 문이 하드 코딩 된 경우에는 응용 프로그램 작성기에서 각 매개 변수의 형식을 이미 알고 있습니다. 런타임에 응용 프로그램에서 SQL 문을 생성 하는 경우 응용 프로그램은 문을 빌드할 때 메타 데이터를 확인할 수 있습니다. 예를 들어 응용 프로그램에서 절을 생성 하는 경우  
  
```  
WHERE OrderID = ?  
```  
  
 OrderID 열에 대해 **Sqlcolumns** 를 호출할 수 있습니다.  
  
 응용 프로그램에서 매개 변수 메타 데이터를 쉽게 확인할 수 없는 유일한 경우는 사용자가 매개 변수가 있는 문을 입력 하는 경우입니다. 이 경우 응용 프로그램은 **Sqlprepare** 를 호출 하 여 문을 준비 하 고 **sqlnumparams** 를 호출 하 여 매개 변수 수를 확인 하 고 각 매개 변수를 설명 하는 **SQLDescribeParam** 을 호출 합니다. 그러나 앞에서 설명한 것 처럼 대부분의 데이터 원본은 드라이버에서 매개 변수 메타 데이터를 검색 하는 방법을 제공 하지 않으므로 **SQLDescribeParam** 는 광범위 하 게 지원 되지 않습니다.

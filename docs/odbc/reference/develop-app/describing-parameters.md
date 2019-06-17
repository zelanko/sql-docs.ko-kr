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
manager: craigg
ms.openlocfilehash: 1bc752afc0cb5214e629a343c35464e612b57c36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049843"
---
# <a name="describing-parameters"></a>매개 변수 설명
**SQLBindParameter** 매개 변수를 설명 하는 인수가: 해당 SQL 형식, 전체 자릿수 및 소수입니다. 이 정보를 사용 하는 드라이버 또는 *메타 데이터를* 매개 변수 값을 데이터 소스에서 필요한 형식으로 변환 합니다. 얼핏 보기에 것 보다 응용 프로그램 매개 변수 메타 데이터를 알고 있는 더 나은 위치에서 드라이버는 어쨌든 드라이버는 결과 집합 열에 대 한 메타 데이터를을 쉽게 검색할 수 있습니다. 결과적으로, 대/소문자 아닙니다. 첫째, 대부분의 데이터 원본 드라이버 매개 변수 메타 데이터를 검색 하는 방법을 제공 하지 않습니다. 둘째, 대부분의 응용 프로그램 메타 데이터를 이미 알고 있습니다.  
  
 SQL 문을 응용 프로그램에 하드 코딩 된 경우 응용 프로그램 작성기 각 매개 변수의 형식을 이미 알고 있습니다. 런타임 시 응용 프로그램에서 SQL 문을 생성 하는 경우 문을 작성 하는 응용 프로그램 메타 데이터를 확인할 수 있습니다. 응용 프로그램은 절을 생성 하는 경우 예를 들어,  
  
```  
WHERE OrderID = ?  
```  
  
 호출할 수 있습니다 **SQLColumns** OrderID 열에 대 한 합니다.  
  
 매개 변수가 있는 문을 입력할 때 응용 프로그램 매개 변수 메타 데이터 확인 쉽게 수 없는 경우에만 표시 합니다. 이 경우 응용 프로그램 호출 **SQLPrepare** 에서 문 준비를 하 **SQLNumParams** 매개 변수의 수를 확인 하 고 **SQLDescribeParam** 설명 하 각 매개 변수입니다. 그러나가 앞에서 설명한 대로 대부분의 데이터 원본은 방법을 제공 하지는 하므로 매개 변수 메타 데이터를 검색 하도록 드라이버에 대 한 **SQLDescribeParam** 광범위 하 게 지원 되지 않습니다.

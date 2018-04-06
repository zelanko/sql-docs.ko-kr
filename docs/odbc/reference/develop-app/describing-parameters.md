---
title: 매개 변수를 설명 하는 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b90b71a5e327e894329ca8474e8edff5740d8826
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="describing-parameters"></a>매개 변수를 설명 하는
**SQLBindParameter** 매개 변수를 설명 하는 인수가: 해당 SQL 유형, 전체 자릿수 및 소수 자릿수입니다. 이 정보를 사용 하는 드라이버 또는 *메타 데이터를* 데이터 원본에 필요한 형식 매개 변수 값으로 변환 해야 합니다. 얼핏 보기에 것 보다 응용 프로그램 매개 변수 메타 데이터를 알고 위치에서 드라이버 임을 즉, 드라이버는 결과 집합 열에 대 한 메타 데이터를 쉽게 검색할 수 있습니다. 결과적으로, 대/소문자 아닙니다. 첫째, 대부분의 데이터 원본 드라이버가 매개 변수 메타 데이터를 검색 하는 방법을 제공 하지 않습니다. 두 번째, 대부분의 응용 프로그램을 이미 알고 있는 메타 데이터입니다.  
  
 응용 프로그램에 하드 코드는 SQL 문이 이면 응용 프로그램 기록기 각 매개 변수의 형식을 이미 알고 있습니다. SQL 문을 실행 시 응용 프로그램에 의해 생성, 응용 프로그램 문을 작성 하는 메타 데이터를 확인할 수 있습니다. 응용 프로그램은 절을 생성 하는 경우 예를 들어  
  
```  
WHERE OrderID = ?  
```  
  
 호출할 수 있는 **SQLColumns** OrderID 열에 대 한 합니다.  
  
 사용자가 매개 변수가 있는 문을 입력할 때 응용 프로그램 매개 변수 메타 데이터 확인 쉽게 수 없는 경우에만 표시 합니다. 이 경우 응용 프로그램 호출 **SQLPrepare** 에서 문 준비를 **SQLNumParams** 매개 변수 수를 결정 하 고 **SQLDescribeParam** 설명 하기 위해 각 매개 변수입니다. 그러나가 앞에서 설명한 대로 대부분의 데이터 원본 방법을 제공 하지 않으므로 하므로 매개 변수 메타 데이터를 검색 하도록 드라이버에 대 한 **SQLDescribeParam** 광범위 하 게 지원 되지 않습니다.

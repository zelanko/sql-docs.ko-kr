---
description: 카탈로그 위치
title: 카탈로그 위치 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 513c2449d296d167c499942636cbb94d637a2ede
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465965"
---
# <a name="catalog-position"></a>카탈로그 위치
식별자에 있는 카탈로그 이름의 위치와 식별자의 나머지와 구분 되는 방법은 데이터 원본에 따라 다릅니다. 예를 들어 Xbase 데이터 원본에서 카탈로그 이름은 디렉터리 이며 Microsoft® Windows®에서 백슬래시 ()로 테이블 이름 (파일 이름)과 구분 됩니다 \\ . 다음 그림에서는이 상황을 보여 줍니다.  
  
 ![카탈로그 위치: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 SQL Server 데이터 원본에서 카탈로그는 데이터베이스 이며 스키마 및 테이블 이름과 마침표 (.)로 구분 됩니다.  
  
 ![카탈로그 위치: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Oracle 데이터 원본에서 카탈로그는 데이터베이스 이기도 하지만 테이블 이름을 따르며 스키마 및 테이블 이름과 함께 기호 (@)로 구분 됩니다.  
  
 ![카탈로그 위치: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 카탈로그 구분 기호 및 카탈로그 이름의 위치를 확인 하기 위해 응용 프로그램은 SQL_CATALOG_NAME_SEPARATOR 및 SQL_CATALOG_LOCATION 옵션으로 **SQLGetInfo** 를 호출 합니다. 상호 운용 가능한 응용 프로그램은 이러한 값에 따라 식별자를 생성 해야 합니다.  
  
 둘 이상의 파트를 포함 하는 식별자를 따옴표로 묶을 때 응용 프로그램은 식별자를 구분 하는 문자를 제외 하 고 각 부분을 인용 하지 않도록 주의 해야 합니다. 예를 들어 다음 문은 Xbase 테이블의 모든 행 및 열을 선택 하 고 카탈로그 (\XBASE\SALES\CORP) 및 테이블 (.dbf) 이름을 인용 하지만 카탈로그 구분 기호 ()는 제외 합니다 \\ .  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 Oracle 테이블의 모든 행 및 열을 선택 하 여 카탈로그 (판매), 스키마 (회사) 및 테이블 (파트) 이름을 선택 하 고 카탈로그 (@) 또는 스키마 (.) 구분 기호는 제외 하는 문은 다음과 같습니다.  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 식별자를 인용 하는 방법에 대 한 자세한 내용은 다음 섹션인 [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)를 참조 하세요.

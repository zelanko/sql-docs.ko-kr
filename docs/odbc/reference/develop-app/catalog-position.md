---
title: "카탈로그 위치 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4b219fe2f008c6e7f0e289211665a1dcf6f1bd1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="catalog-position"></a>카탈로그 위치
데이터 원본에 데이터 원본의 식별자 및 식별자의 나머지 부분에서 어떻게 분리 되는지에서 카탈로그 이름의 위치 달라 집니다. 예를 들어 Xbase 데이터 원본에 카탈로그 이름이 디렉터리와, Microsoft® Windows®에서 구별 (즉, 파일 이름) 테이블 이름에 백슬래시가 (\\). 다음 그림에서는이 문제를 보여 줍니다.  
  
 ![카탈로그 위치: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 SQL Server 데이터 원본에서 카탈로그 데이터베이스 이며 스키마와 테이블 이름에서 마침표 (.)으로 구분 됩니다.  
  
 ![카탈로그 위치: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Oracle 데이터 원본에서 카탈로그 데이터베이스 이기도 하지만 테이블 이름 뒤에 오는 구별 하 여 스키마 및 테이블 이름을 at 기호 (@).  
  
 ![카탈로그 위치: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 카탈로그 구분 기호 및 카탈로그 이름의 위치를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 및 SQL_CATALOG_LOCATION 옵션입니다. 상호 운용 가능한 응용 프로그램에는 이러한 값에 따라 식별자 생성 해야 합니다.  
  
 둘 이상의 부분을 포함 하는 식별자를 따옴표로 묶는 경우 응용 프로그램을 각 부분을 별도로 quote 하지 식별자를 구분 하는 문자를 따옴표 주의 해야 합니다. 예를 들어 모든 행과 Xbase 테이블의 열 선택 하려면 다음 문을 있는 값을 따옴표로 카탈로그 (\XBASE\SALES\CORP) 및 (Parts.dbf) 테이블 이름이 있지만 카탈로그 구분 (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 모든 행과 Oracle 테이블의 열 선택 하려면 다음 문을 따옴표 카탈로그 (판매), (회사), 스키마 및 테이블 (부분) 이름 하지만 카탈로그 없습니다 (@) 또는 스키마 (.) 구분:  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 따옴표 식별자에 대 한 내용은 다음 섹션을 참조 하십시오. [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)합니다.

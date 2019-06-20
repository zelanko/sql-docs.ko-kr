---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22a9a9d50891a6101076af6378fb33543274b21b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63237935"
---
# <a name="catalog-position"></a>카탈로그 위치
데이터 원본에 데이터 원본의 식별자 및 식별자의 나머지 부분에서 분리 하는 방식을 카탈로그 이름의 위치가 달라 집니다. 예를 들어, Xbase 데이터 소스의 카탈로그 이름을 디렉터리 이며, Microsoft® Windows®에서 구분 된 테이블 이름 (즉, 파일 이름)에서 백슬래시 (\\). 다음 그림에서는이 문제를 보여 줍니다.  
  
 ![카탈로그 위치: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 SQL Server 데이터 원본에서 카탈로그는 데이터베이스 및 스키마와 테이블 이름에서 마침표 (.)로 구분 됩니다.  
  
 ![카탈로그 위치: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Oracle 데이터 원본에서 카탈로그 데이터베이스 이기도 하지만 테이블 이름 다음에 나오는 구별 하 여 스키마와 테이블 이름은 at 기호 (@).  
  
 ![카탈로그 위치: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 카탈로그 구분 기호 및 카탈로그 이름의 위치를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 및 SQL_CATALOG_LOCATION 옵션을 사용 하 여 합니다. 상호 운용 가능한 응용 프로그램에는 이러한 값에 따라 식별자 생성 해야 합니다.  
  
 둘 이상의 파트가 포함 된 식별자, 인용 하는 경우 응용 프로그램을 개별적으로 각 부분을 인용 식별자를 구분 하는 문자를 하지 인용 주의 해야 합니다. 모든 행 및 Xbase 테이블의 열을 선택 하려면 다음 문을 카탈로그 (\XBASE\SALES\CORP) 및 (Parts.dbf) 테이블 이름 이지만 카탈로그 구분 기호가 없습니다 따옴표 하는 예를 들어 (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 모든 행 및 Oracle 테이블의 열을 선택 하려면 다음 문을 따옴표 (Sales) 카탈로그, 스키마 (회사) 하며 (부분) 테이블 이름을 카탈로그 없습니다 (@) 또는 스키마 (.) 구분:  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 따옴표 식별자에 대 한 내용은 다음 섹션을 참조 하세요 [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)합니다.

---
title: 카탈로그 위치 | 마이크로 소프트 문서
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
ms.openlocfilehash: 0305d978dc4ecd21892a0be3916fa5072b7be95a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303384"
---
# <a name="catalog-position"></a>카탈로그 위치
식별자에서 카탈로그 이름의 위치와 식별자의 나머지 부분과 분리되는 방법은 데이터 원본마다 다릅니다. 예를 들어 Xbase 데이터 원본에서 카탈로그 이름은 디렉터리이며 Microsoft® Windows® 백슬래시()로\\테이블 이름(파일 이름)과 분리됩니다. 다음 그림에서는 이 상태를 보여 줍니다.  
  
 ![카탈로그 위치: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 SQL Server 데이터 원본에서 카탈로그는 데이터베이스이며 마침표(.)로 스키마 및 테이블 이름과 분리됩니다.  
  
 ![카탈로그 위치: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Oracle 데이터 원본에서 카탈로그는 데이터베이스이기도 하지만 테이블 이름을 따르며 스키마 및 테이블 이름과 at sign(@)으로 구분됩니다.  
  
 ![카탈로그 위치: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 카탈로그 구분 기호와 카탈로그 이름의 위치를 확인하려면 응용 프로그램에서 SQL_CATALOG_NAME_SEPARATOR 및 SQL_CATALOG_LOCATION 옵션을 사용하여 **SQLGetInfo를** 호출합니다. 상호 운용 가능한 응용 프로그램은 이러한 값에 따라 식별자를 생성해야 합니다.  
  
 두 개 이상의 부품을 포함하는 식별자를 인용할 때 응용 프로그램은 각 부품을 따로 인용하고 식별자를 구분하는 문자를 인용하지 않도록 주의해야 합니다. 예를 들어 Xbase 테이블의 모든 행과 열을 선택하는 다음 문은 카탈로그(\XBASE\SALES\CORP) 및 테이블(Parts.dbf) 이름을 따로 따로\\따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따로 따옴표를 그리며 카탈로그 구분 기호 ()  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 Oracle 테이블의 모든 행과 열을 선택하는 다음 문은 카탈로그(@) 또는 스키마(.) 구분 기호가 아닌 카탈로그(Sales), 스키마(회사) 및 테이블(부품) 이름을 인용합니다.  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 식별자를 인용하는 것에 대한 자세한 내용은 다음 섹션, [따옴표 식별자를](../../../odbc/reference/develop-app/quoted-identifiers.md)참조하십시오.

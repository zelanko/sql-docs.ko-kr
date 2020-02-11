---
title: 카탈로그 및 스키마 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e10460df120451502d798376453d69d111051ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064409"
---
# <a name="catalog-and-schema-usage"></a>카탈로그 및 스키마 사용
데이터 원본에서는 모든 SQL 문의 개체 이름 식별자로 카탈로그 및 스키마 이름을 지원 하지 않아도 됩니다. 데이터 원본은 다음과 같은 SQL 문 클래스 중 하나 이상에서 카탈로그 및 스키마 이름을 지원할 수 있습니다. DML (데이터 조작 언어) 문, 프로시저 호출, 테이블 정의 문, 인덱스 정의 문 및 권한 정의 할당문. 카탈로그 및 스키마 이름을 사용할 수 있는 SQL 문의 클래스를 확인 하기 위해 응용 프로그램은 SQL_CATALOG_USAGE 및 SQL_SCHEMA_USAGE 옵션으로 **SQLGetInfo** 를 호출 합니다.

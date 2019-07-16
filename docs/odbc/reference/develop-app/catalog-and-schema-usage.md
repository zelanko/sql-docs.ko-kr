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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064409"
---
# <a name="catalog-and-schema-usage"></a>카탈로그 및 스키마 사용
데이터 원본을 지원 하지 않을 카탈로그 및 스키마 이름이 모든 SQL 문에서 개체 이름 식별자로. 데이터 원본은 수 SQL 문의 다음 클래스 중 하나 이상의 카탈로그 이름과 스키마를 지원 합니다. 데이터 조작 언어 (DML) 문, 프로시저 호출, 테이블 정의 문, 인덱스 정의 문 및 권한 정의 문 카탈로그 및 스키마 이름을 사용할 수는 SQL 문 클래스를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_CATALOG_USAGE 및 SQL_SCHEMA_USAGE 옵션을 사용 하 여 합니다.

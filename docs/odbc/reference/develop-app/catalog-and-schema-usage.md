---
title: 카탈로그 및 스키마 사용 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 245bd007f070a94689283830ba7a1362e31353e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306254"
---
# <a name="catalog-and-schema-usage"></a>카탈로그 및 스키마 사용
데이터 원본이 카탈로그 및 스키마 이름을 모든 SQL 문에서 개체 이름 식별자로 반드시 지원하지는 않습니다. 데이터 원본은 DML(데이터 조작 언어) 명령문, 프로시저 호출, 테이블 정의 문, 인덱스 정의 문 및 권한 정의 문 중 하나 이상의 SQL 문 클래스에서 카탈로그 및 스키마 이름을 지원할 수 있습니다. 카탈로그 및 스키마 이름을 사용할 수 있는 SQL 문의 클래스를 확인하려면 응용 프로그램에서 SQL_CATALOG_USAGE 및 SQL_SCHEMA_USAGE 옵션을 사용하여 **SQLGetInfo를** 호출합니다.

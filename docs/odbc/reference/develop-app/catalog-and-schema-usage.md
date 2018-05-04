---
title: 카탈로그 및 스키마 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f0295ee92c6fed4690f33691037e58fe0ae951a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-and-schema-usage"></a>카탈로그 및 스키마 사용
데이터 소스를 지원 하지 않을 카탈로그와 스키마 이름이 모든 SQL 문에서 개체 이름 식별자로. SQL 문의 다음 클래스 중 하나 이상에 데이터 원본 카탈로그와 스키마 이름이 지원할 수 있습니다: 조작 DML (데이터 언어) 문, 프로시저 호출, 테이블 정의 문, 인덱스 정의 문 및 권한 정의 문입니다. 응용 프로그램 카탈로그와 스키마 이름은 사용할 수 있습니다 하는 SQL 문 클래스를 확인 하려면 호출 **SQLGetInfo** SQL_CATALOG_USAGE 및 SQL_SCHEMA_USAGE 옵션입니다.

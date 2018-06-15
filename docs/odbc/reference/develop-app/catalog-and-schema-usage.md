---
title: 카탈로그 및 스키마 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 0aa8e5c112bbd3bc807ecba821da2e754016b23a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907248"
---
# <a name="catalog-and-schema-usage"></a>카탈로그 및 스키마 사용
데이터 소스를 지원 하지 않을 카탈로그와 스키마 이름이 모든 SQL 문에서 개체 이름 식별자로. SQL 문의 다음 클래스 중 하나 이상에 데이터 원본 카탈로그와 스키마 이름이 지원할 수 있습니다: 조작 DML (데이터 언어) 문, 프로시저 호출, 테이블 정의 문, 인덱스 정의 문 및 권한 정의 문입니다. 응용 프로그램 카탈로그와 스키마 이름은 사용할 수 있습니다 하는 SQL 문 클래스를 확인 하려면 호출 **SQLGetInfo** SQL_CATALOG_USAGE 및 SQL_SCHEMA_USAGE 옵션입니다.

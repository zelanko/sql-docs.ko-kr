---
title: SQLGetTypeInfo를 사용하여 데이터 형식 정보 검색 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec2bbba824eaf3d74133cf9754eca2593c9fb79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300063"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>SQLGetTypeInfo를 사용하여 데이터 형식 정보 검색
기본 SQL 데이터 형식에서 ODBC 형식 식별자에 대한 매핑은 근사치이므로 ODBC는 드라이버가 데이터 원본의 각 SQL 데이터 형식을 완전히 설명할 수 있는**함수(SQLGetTypeInfo)를**제공합니다. 이 함수는 이름, 형식 식별자, 정밀도, 축척 및 nullability와 같은 단일 데이터 형식의 특성을 설명하는 각 행에 대한 결과 집합을 반환합니다.  
  
 이 정보는 일반적으로 사용자가 테이블을 만들고 변경할 수 있도록 하는 일반 응용 프로그램에서 사용됩니다. 이러한 응용 프로그램은 **SQLGetTypeInfo를** 호출하여 데이터 형식 정보를 검색한 다음 일부 또는 전부를 사용자에게 제공합니다. 이러한 응용 프로그램은 다음 두 가지를 알고 있어야 합니다.  
  
-   두 개 이상의 SQL 데이터 형식이 단일 형식 식별자에 매핑될 수 있으므로 사용할 데이터 형식을 결정하기가 어려울 수 있습니다. 이 문제를 해결하기 위해 결과 집합은 먼저 형식 식별자별로 정렬되고 두 번째는 형식 식별자의 정의에 가깝게 정렬됩니다. 또한 데이터 원본 정의 데이터 형식이 사용자 정의 데이터 형식보다 우선합니다. 예를 들어 데이터 원본이 COUNTER가 자동 증분이라는 점을 제외하면 데이터 원본이 정수 및 COUNTER 데이터 형식을 동일하게 정의한다고 가정합니다. 사용자 정의 형식 WHOLENUM이 정수기의 동의어라고 가정해 보도록 합니다. 이러한 각 유형은 SQL_INTEGER 맵을 매핑합니다. **SQLGetTypeInfo** 결과 집합에서 정수 먼저 나타나고 WHOLENUM 다음에 카운터가 나타납니다. WHOLENUM은 사용자 정의이기 때문에 정수 후에 나타나지만 SQL_INTEGER 형식 식별자의 정의와 더 밀접하게 일치하기 때문에 COUNTER 앞에 나타납니다.  
  
-   ODBC는 **CREATE TABLE** 및 **ALTER TABLE** 문에서 사용할 데이터 형식 이름을 정의하지 않습니다. 대신 응용 프로그램은 **SQLGetTypeInfo에서**반환한 결과 집합의 TYPE_NAME 열에 반환된 이름을 사용해야 합니다. 그 이유는 대부분의 SQL이 DBMS마다 크게 다르지 는 않지만 데이터 형식 이름이 크게 다르기 때문입니다. ODBC는 드라이버가 SQL 문을 구문 분석하고 표준 데이터 형식 이름을 DBMS 별 데이터 형식 이름으로 바꾸도록 하는 대신 응용 프로그램에서 DBMS 관련 이름을 먼저 사용해야 합니다.  
  
 **SQLGetTypeInfo는** 반드시 응용 프로그램에서 발생할 수 있는 모든 데이터 형식을 설명 하지 않습니다. 특히 결과 집합에는 데이터 원본에서 직접 지원하지 않는 데이터 형식이 포함될 수 있습니다. 예를 들어 카탈로그 함수에서 반환되는 결과 집합의 열 데이터 형식은 ODBC에 의해 정의되며 이러한 데이터 형식은 데이터 원본에서 지원되지 않을 수 있습니다. 결과 집합에서 데이터 형식의 특성을 확인 하려면 응용 프로그램에서 **SQLColAttribute**를 호출 합니다.

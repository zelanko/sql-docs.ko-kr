---
title: SQLGetTypeInfo를 사용 하 여 데이터 형식 정보 검색 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300063"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>SQLGetTypeInfo를 사용하여 데이터 형식 정보 검색
기본 SQL 데이터 형식에서 ODBC 형식 식별자로의 매핑은 근사값 이므로 ODBC는 드라이버에서 데이터 원본의 각 SQL 데이터 형식을 완전히 설명할 수 있는 함수 (**SQLGetTypeInfo**)를 제공 합니다. 이 함수는 이름, 형식 식별자, 전체 자릿수, 소수 자릿수 및 null 허용 여부와 같은 단일 데이터 형식의 특징을 설명 하는 각 행의 결과 집합을 반환 합니다.  
  
 이 정보는 일반적으로 사용자가 테이블을 만들고 변경할 수 있도록 하는 일반 응용 프로그램에서 사용 됩니다. 이러한 응용 프로그램은 **SQLGetTypeInfo** 를 호출 하 여 데이터 형식 정보를 검색 한 다음이 정보 중 일부 또는 모두를 사용자에 게 제공 합니다. 이러한 응용 프로그램은 다음 두 가지를 인식 해야 합니다.  
  
-   두 개 이상의 SQL 데이터 형식이 단일 형식 식별자에 매핑될 수 있으므로 사용할 데이터 형식을 결정 하기가 어려울 수 있습니다. 이를 해결 하기 위해 결과 집합은 먼저 형식 식별자를 기준으로 정렬 되 고 두 번째는 형식 식별자의 정의를 거리 하 여 정렬 됩니다. 또한 데이터 원본 정의 데이터 형식이 사용자 정의 데이터 형식 보다 우선적으로 적용 됩니다. 예를 들어, 데이터 소스는 카운터가 자동 증분을 제외 하 고 정수 및 카운터 데이터 형식을 동일 하 게 정의 한다고 가정 합니다. 또한 사용자 정의 형식 WHOLENUM은 정수의 동의어 라고 가정 합니다. 이러한 형식은 각각 SQL_INTEGER에 매핑됩니다. **SQLGetTypeInfo** 결과 집합에서 정수는 먼저 표시 되 고 그 뒤에 WHOLENUM와 카운터를 차례로 표시 합니다. WHOLENUM은 사용자가 정의 하는 것이 고, 카운터 앞에는 SQL_INTEGER 형식 식별자의 정의와 더 밀접 하 게 일치 하므로 정수 뒤에 나타납니다.  
  
-   ODBC는 **CREATE TABLE** 및 **ALTER TABLE** 문에 사용할 데이터 형식 이름을 정의 하지 않습니다. 대신 응용 프로그램은 **SQLGetTypeInfo**에서 반환 된 결과 집합의 TYPE_NAME 열에 반환 되는 이름을 사용 해야 합니다. 그 이유는 대부분의 SQL이 Dbms에서 크게 다르지 않지만 데이터 형식 이름은 크게 다릅니다. 드라이버를 사용 하 여 SQL 문을 구문 분석 하 고 표준 데이터 형식 이름을 DBMS 관련 데이터 형식 이름으로 대체 하는 대신 ODBC에서는 응용 프로그램에서 DBMS 관련 이름을 먼저 사용 해야 합니다.  
  
 **SQLGetTypeInfo** 는 응용 프로그램에서 발생할 수 있는 모든 데이터 형식을 반드시 설명 하지는 않습니다. 특히 결과 집합에는 데이터 원본에서 직접 지원 하지 않는 데이터 형식이 포함 될 수 있습니다. 예를 들어 카탈로그 함수에서 반환 하는 결과 집합의 열 데이터 형식은 ODBC에 의해 정의 되며 데이터 원본에서 지원 되지 않을 수 있습니다. 응용 프로그램은 결과 집합에 있는 데이터 형식의 특성을 확인 하기 위해 **Sqlcolattribute**를 호출 합니다.

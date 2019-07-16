---
title: SQLGetTypeInfo 사용 하 여 정보를 입력 하는 데이터를 검색할 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4f336a7ebfaf5e76ac464944900231c452809f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020552"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>SQLGetTypeInfo를 사용하여 데이터 형식 정보 검색
ODBC 형식 식별자로 SQL 데이터 형식에서 매핑을 대략적인 이기 때문에 ODBC 함수를 제공 하는 (**SQLGetTypeInfo**)는 드라이버 수 완전히를 통해 데이터 소스에서 각 SQL 데이터 형식에 설명 합니다. 이 함수는 각 행에는 단일 데이터 형식 이름, 형식 식별자, 전체 자릿수, 소수 자릿수 및 null 허용 여부 등의 특징을 설명 하는 결과 집합을 반환 합니다.  
  
 이 정보는 일반적으로 사용자를 만들고 테이블을 변경할 수 있도록 하는 일반 응용 프로그램에서 사용 됩니다. 이러한 응용 프로그램 호출 **SQLGetTypeInfo** 를 데이터 형식 정보를 검색 한 다음 사용자에 게 일부 또는 모두를 제공 합니다. 이러한 응용 프로그램은 두 가지에 유의 해야 합니다.  
  
-   둘 이상의 SQL 데이터 형식을 사용할 데이터 형식을 결정 하기 어려울 수 있는 단일 형식 식별자를 매핑할 수 있습니다. 이 해결 하기 위해 결과 집합 유형 식별자 고 두 번째 유형 식별자의 정의를 선택 하 여 먼저 정렬 됩니다. 또한 데이터 원본 정의 데이터 형식이 사용자 정의 데이터 형식 보다 우선적으로 적용 합니다. 예를 들어, 카운터는 자동 증가 한다는 점을 제외 하면 동일 하도록 카운터 데이터 형식과 정수 데이터 소스를 정의 하는 합니다. 또한 사용자 정의 형식이 WHOLENUM 정수의 동의어 임을 가정 합니다. 이러한 각 유형의 SQL_INTEGER 매핑됩니다. 에 **SQLGetTypeInfo** 결과 집합, 정수 WHOLENUM 뒤에 먼저 표시 되 고 다음 카운터입니다. 사용자 정의 하지만 카운터 전에 일치 하기 때문에 더 밀접 하 게 정의 된 SQL_INTEGER의 식별자를 입력 하기 때문에 정수 뒤 WHOLENUM에 표시 됩니다.  
  
-   ODBC 데이터 형식에서 이름을 정의 하지 않습니다 **CREATE TABLE** 하 고 **ALTER TABLE** 문입니다. 대신, 응용 프로그램에서 반환한 결과 집합의 TYPE_NAME 열에서 반환 되는 이름을 사용할지 **SQLGetTypeInfo**합니다. 이 대 한 이유는 대부분 SQL의 Dbms 간에 많은 달라 지지 않습니다 하지만 데이터 형식 이름은 다릅니다 단시간입니다. SQL 문을 구문 분석 및 DBMS 특정 데이터 형식 이름을 사용 하 여 표준 데이터 형식 이름 바꾸기에 드라이버를 요구 하는 대신 ODBC에는 처음에 DBMS 특정 이름을 사용 하도록 응용 프로그램에 필요 합니다.  
  
 사실은 **SQLGetTypeInfo** 모든 응용 프로그램에서 발생할 수 있는 데이터 형식을 반드시 설명 하지 않습니다. 특히 결과 집합에는 직접 지원 되지 않는 데이터 원본에서 데이터 형식을 포함할 수 있습니다. 예를 들어, ODBC에서 정의 된 카탈로그 함수에 의해 반환 된 결과 집합의 열 데이터 형식 및 이러한 데이터 형식은 데이터 원본에서 지원 되지 않는 합니다. 결과 집합의 데이터 형식과의 특징을 확인 하려면 응용 프로그램 호출 **SQLColAttribute**합니다.

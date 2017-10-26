---
title: "데이터를 검색할 SQLGetTypeInfo 사용 하 여 정보를 입력 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8a1eb337e91595b5be013067847f73c3de117e97
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>SQLGetTypeInfo와 데이터 형식 정보를 검색 하는 중
ODBC 함수를 제공 이기 때문에 기본 SQL 데이터 형식 ODBC 형식 식별자 매핑을 대략적인 (**SQLGetTypeInfo**) 하는 드라이버 수 완전히를 통해 데이터 원본에서 각 SQL 데이터 형식에 설명 합니다. 이 함수는 결과 집합을 단일 데이터 형식, 이름, 유형 식별자, 전체 자릿수, 소수 자릿수 및 null 허용 여부 등의 특성을 설명 하는 각 행을 반환 합니다.  
  
 일반적으로이 정보는 사용자가을 만들고 테이블을 변경할 수 있는 일반 응용 프로그램에서 사용 됩니다. 이러한 응용 프로그램 호출 **SQLGetTypeInfo** 를 데이터 형식 정보를 검색 한 다음 사용자에 게 일부 또는 모두를 제공 합니다. 이러한 응용 프로그램에서는 다음 두 가지 중 알고 있어야 합니다.  
  
-   둘 이상의 SQL 데이터 형식을 사용 하도록 데이터 형식을 결정 하기 어려울 수 있습니다. 있는 단일 형식 식별자를 매핑할 수 있습니다. 이 해결 하기 위해 결과 집합 유형 식별자 및 두 번째 거리 유형 식별자의 정의를 먼저 정렬 됩니다. 또한 데이터 원본에서 정의 된 데이터 형식 우선 사용자 정의 데이터 형식입니다. 예를 들어 데이터 원본 카운터는 자동 증가 한다는 점을 제외 하면 동일 해야 정수와 카운터 데이터 형식을 정의 하는 것으로 가정 합니다. 또한 사용자 정의 형식이 WHOLENUM 정수의 동의어 임을 가정 합니다. 이러한 각 유형의 SQL_INTEGER에 매핑됩니다. 에 **SQLGetTypeInfo** 결과 집합, 정수 WHOLENUM 이어서 먼저 표시 하 고 다음 카운터입니다. 사용자 정의 하지만 카운터 하기 전에 일치 하기 때문에 더 밀접 하 게 정의 SQL_INTEGER의 식별자를 입력 하기 때문에 정수 뒤 WHOLENUM에 표시 됩니다.  
  
-   ODBC 데이터 형식에서 이름을 정의 하지 않습니다 **CREATE TABLE** 및 **ALTER TABLE** 문. 대신 응용 프로그램에서 반환 된 결과 집합의 TYPE_NAME 열에서 반환 되는 이름을 사용 해야 **SQLGetTypeInfo**합니다. 이유는는 대부분 SQL의 Dbms 간에 많은 달라 지지 않습니다 이지만 데이터 형식 이름은 가격은 매우 다양 합니다. SQL 문을 구문 분석 및 DBMS 특정 데이터 형식 이름은 표준 데이터 형식 이름 바꾸기는 드라이버를 요구 하는 대신 ODBC 응용 프로그램 이름을 사용 하는 특정 DBMS 처음에 필요 합니다.  
  
 **SQLGetTypeInfo** 모든 응용 프로그램에서 발생할 수 있는 데이터 형식을 반드시 설명 하지 않습니다. 특히 결과 집합에는 직접 지원 되지 않는 데이터 원본에서 데이터 형식을 포함할 수 있습니다. 예를 들어 ODBC 카탈로그 함수에서 반환 된 결과 집합에 있는 열의 데이터 형식을 정의 합니다 및 이러한 데이터 형식은 데이터 원본에서 지원 되지 않는 합니다. 결과 집합에 속하는 데이터 형식 특성을 확인 하려면 응용 프로그램이 호출 **SQLColAttribute**합니다.


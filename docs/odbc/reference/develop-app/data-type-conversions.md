---
description: 데이터 형식 변환
title: 데이터 형식 변환 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92c31cb12c7bb02cf8e108251ae5ebd6f12aed5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429345"
---
# <a name="data-type-conversions"></a>데이터 형식 변환
다음 중 한 가지 방법으로 데이터를 한 형식에서 다른 형식으로 변환할 수 있습니다. 데이터를 한 응용 프로그램 변수에서 다른 응용 프로그램 변수 (C에서 C로)로 전송 하는 경우, 응용 프로그램 변수의 데이터가 문 매개 변수 (C에서 SQL로)로 전송 되 고, 결과 집합 열의 데이터가 응용 프로그램 변수 (SQL에서 C로)로 전송 되는 경우 및 데이터 원본 열 간에 데이터가 전송 될 때 (SQL에서 sql로)  
  
 한 응용 프로그램 변수에서 다른 응용 프로그램 변수로 데이터를 전송할 때 발생 하는 변환은이 문서의 범위를 벗어납니다.  
  
 응용 프로그램에서 결과 집합 열 또는 문 매개 변수에 변수를 바인딩할 때 응용 프로그램은 응용 프로그램 변수의 데이터 형식 선택에 따라 데이터 형식 변환을 암시적으로 지정 합니다. 예를 들어 열에 정수 데이터가 포함 되어 있다고 가정 합니다. 응용 프로그램이 정수 변수를 열에 바인딩하는 경우에는 변환이 수행 되지 않도록 지정 합니다. 응용 프로그램에서 문자 변수를 열에 바인딩하는 경우 데이터를 정수에서 문자로 변환 하도록 지정 합니다.  
  
 ODBC는 각 SQL 및 C 데이터 형식 간에 데이터를 변환 하는 방법을 정의 합니다. 기본적으로 ODBC는 문자-정수, 정수에서 부동으로의 모든 적절 한 변환을 지원 하며 float to date와 같이 잘못 정의 된 변환을 지원 하지 않습니다. 드라이버가 지 원하는 각 SQL 데이터 형식에 대 한 모든 변환을 지원 하려면 드라이버가 필요 합니다. SQL 및 C 데이터 형식 간의 전체 변환 목록은 [sql에서 c 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 및 부록 D: 데이터 형식에서 데이터를 [c에서 sql 데이터 형식으로 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 을 참조 하세요.  
  
 또한 ODBC는 데이터를 한 SQL 데이터 형식에서 다른 형식으로 변환 하는 스칼라 함수를 정의 합니다. **CONVERT** 스칼라 함수는 데이터 원본에서 변환을 수행 하기 위해 정의 된 기본 스칼라 함수 또는 함수에 드라이버에 의해 매핑됩니다. 이 함수는 DBMS 관련 함수에 매핑되므로 ODBC는 이러한 변환의 작동 방식 또는 지원 되는 변환을 정의 하지 않습니다. 응용 프로그램은 **SQLGetInfo**의 SQL_CONVERT 옵션을 통해 특정 드라이버 및 데이터 원본에서 지원 되는 변환을 검색 합니다. **CONVERT** 스칼라 함수에 대 한 자세한 내용은 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 및 [명시적 데이터 형식 변환 함수](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)를 참조 하세요.

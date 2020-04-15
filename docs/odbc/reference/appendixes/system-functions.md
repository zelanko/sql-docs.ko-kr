---
title: 시스템 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca71687887444cafc502c15683f3972cf6308e6b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302834"
---
# <a name="system-functions"></a>시스템 함수
다음 표에는 ODBC 스칼라 함수 집합에 포함된 시스템 함수가 나열되어 있습니다. SQL_SYSTEM_FUNCTIONS *정보 유형으로* **SQLGetInfo를** 호출하여 응용 프로그램은 드라이버에서 지원하는 시스템 함수를 결정할 수 있습니다.  
  
 *exp로* 표시된 인수는 열의 이름, 다른 스칼라 함수의 결과 또는 기본 데이터 형식을 SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP 나타낼 수 있는 리터럴일 수 있습니다.  
  
 *값으로* 표시된 인수는 기본 데이터 형식을 SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP 나타낼 수 있는 리터럴 상수일 수 있습니다.  
  
 반환되는 값은 ODBC 데이터 유형으로 표시됩니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**데이터베이스(ODBC** 1.0)|연결 핸들에 해당하는 데이터베이스 이름을 반환합니다. 데이터베이스 이름은 SQL_CURRENT_QUALIFIER 연결 옵션으로 **SQLGetConnectOption을** 호출하여 사용할 수도 있습니다.|  
|**IFNULL(exp** _exp_,_값)_**)** (ODBC 1.0)|*exp가* null이면 *값이* 반환됩니다. *exp가* null이 아닌 경우 *exp가* 반환됩니다. 가능한 데이터 형식 또는 *값* 유형은 *exp의*데이터 형식과 호환되어야 합니다.|  
|**사용자(ODBC** 1.0)|DBMS에서 사용자 이름을 반환합니다. (사용자 이름은 정보 형식을 지정하여 **SQLGetInfo를** 통해 사용할 수 SQL_USER_NAME.) 이는 로그인 이름과 다를 수 있습니다.|

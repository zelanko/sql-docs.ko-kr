---
title: 시스템 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 048db455419d2b74658b758f3a3c525b02bf37f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811411"
---
# <a name="system-functions"></a>시스템 함수
다음 표에서 ODBC 스칼라 함수 집합에 포함 된 시스템 함수를 나열 합니다. 호출 하 여 **SQLGetInfo** 사용 하 여는 *정보 유형* SQL_SYSTEM_FUNCTIONS의 응용 프로그램을 드라이버에서 지원 되는 시스템 함수 확인할 수 있습니다.  
  
 로 표시 된 인수 *exp* SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL 기본 데이터 형식이 표시 될 수 있습니다 위치 열, 다른 스칼라 함수 또는 리터럴, 결과의 이름일 수 있습니다 _BIGINT SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP 합니다.  
  
 로 표시 된 인수 *값* SQL_NUMERIC SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_로 기본 데이터 형식을 나타낼 수 있는 리터럴 상수를 수 있습니다 TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP 합니다.  
  
 반환 되는 값은 ODBC 데이터 형식으로 표시 됩니다.  
  
|기능|Description|  
|--------------|-----------------|  
|**데이터베이스 ()** (ODBC 1.0)|연결 핸들에 해당 데이터베이스의 이름을 반환 합니다. (호출 하 여 데이터베이스의 이름을 사용할 수 있는 이기도 **SQLGetConnectOption** SQL_CURRENT_QUALIFIER 연결 옵션을 사용 하 여.)|  
|**IFNULL (** *exp*하십시오*값 * * *)** (ODBC 1.0)|하는 경우 *exp* 가 null *값* 반환 됩니다. 하는 경우 *exp* null이 아니면 *exp* 반환 됩니다. 가능한 데이터 형식 또는 형식의 *값* 데이터 형식과 호환 되어야 *exp*합니다.|  
|**사용자 ()** (ODBC 1.0)|DBMS의 사용자 이름을 반환 합니다. (사용자 이름은 또한의 방식으로 사용할 수 있습니다 **SQLGetInfo** 정보 형식을 지정 하 여: SQL_USER_NAME.) 로그인 이름과 다를 수 있습니다.|

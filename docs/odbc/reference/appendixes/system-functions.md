---
title: "시스템 함수 | Microsoft Docs"
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
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1537c769de2c0f421ed533ea73d75a1578a10559
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="system-functions"></a>시스템 함수
다음 표에서 ODBC 스칼라 함수 집합에 포함 된 시스템 함수를 나열 합니다. 호출 하 여 **SQLGetInfo** 와 *정보 유형* SQL_SYSTEM_FUNCTIONS의 응용 프로그램이 드라이버를 통해 지원 되는 시스템 함수 확인할 수 있습니다.  
  
 로 표시 된 인수 *exp* SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL 기본 데이터 형식을 나타낼 수 있습니다 위치 열, 다른 스칼라 함수 또는 리터럴, 결과의 이름이 될 수 있습니다 _BIGINT, SQL_FLOAT SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP 합니다.  
  
 로 표시 된 인수 *값* SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_로 기본 데이터 형식을 나타낼 수 있는 리터럴 상수를 사용할 수 있습니다 TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP 합니다.  
  
 반환 값은 ODBC 데이터 형식으로 표시 됩니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**데이터베이스 ()** (ODBC 1.0)|연결 핸들에 해당 하는 데이터베이스의 이름을 반환 합니다. (호출 하 여 데이터베이스의 이름을 사용할 수 있는 이기도 **SQLGetConnectOption** SQL_CURRENT_QUALIFIER 연결 옵션을 사용 합니다.)|  
|**IFNULL (** *exp*,*값***)** (ODBC 1.0)|경우 *exp* 매개 변수가 null 이면 *값* 반환 됩니다. 경우 *exp* null이 아니면 *exp* 반환 됩니다. 가능한 데이터 형식이 나 형식의 *값* 의 데이터 형식과 호환 되어야 합니다 *exp*합니다.|  
|**사용자 ()** (ODBC 1.0)|DBMS의 사용자 이름을 반환 합니다. (사용자 이름을 통해 제공 됩니다. **SQLGetInfo** 정보 유형을 지정 하 여: SQL_USER_NAME.) 로그인 이름과 다를 수 있습니다.|

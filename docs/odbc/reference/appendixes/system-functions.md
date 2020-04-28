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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca71687887444cafc502c15683f3972cf6308e6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302834"
---
# <a name="system-functions"></a>시스템 함수
다음 표에서는 ODBC 스칼라 함수 집합에 포함 된 시스템 함수를 보여 줍니다. 응용 프로그램에서는 *정보 형식이* SQL_SYSTEM_FUNCTIONS 인 **SQLGetInfo** 를 호출 하 여 드라이버에서 지원 되는 시스템 함수를 확인할 수 있습니다.  
  
 *Exp* 로 표시 되는 인수는 열 이름, 다른 스칼라 함수의 결과 또는 기본 데이터 형식이 SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP으로 표시 될 수 있는 리터럴입니다.  
  
 *Value* 로 표시 되는 인수는 리터럴 상수일 수 있습니다. 여기서 기본 데이터 형식은 SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP로 표시 될 수 있습니다.  
  
 반환 되는 값은 ODBC 데이터 형식으로 표시 됩니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**DATABASE ()** (ODBC 1.0)|연결 핸들에 해당 하는 데이터베이스의 이름을 반환 합니다. 데이터베이스 이름은 SQL_CURRENT_QUALIFIER 연결 옵션을 사용 하 여 **SQLGetConnectOption** 를 호출 하 여 사용할 수도 있습니다.|  
|**Ifnull (** _exp_,_value_**)** (ODBC 1.0)|*Exp* 가 null 인 경우 *값* 이 반환 됩니다. *Exp* 가 null이 아닌 경우 *exp* 가 반환 됩니다. 가능한 데이터 형식 또는 *값* 유형은 *exp*의 데이터 형식과 호환 되어야 합니다.|  
|**USER ()** (ODBC 1.0)|DBMS의 사용자 이름을 반환 합니다. 사용자 이름은 SQL_USER_NAME 정보 유형을 지정 하 여 **SQLGetInfo** 에서 사용할 수도 있습니다. 이 이름은 로그인 이름과 다를 수 있습니다.|

---
title: 일반 인수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 997604b4376656d36d2bc4bc31f1959aa6c8a229
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987823"
---
# <a name="ordinary-arguments"></a>일반 인수
카탈로그 함수 문자열 인수가 일반 인수 경우 리터럴 문자열로 처리 됩니다. 일반 인수 문자열 검색 패턴을 아니고 값 목록을 허용합니다. 일반 인수의 경우 유효 하 고 문자열에 인용 문자는 문자 그대로 해석 됩니다. SQL_ATTR_METADATA_ID 문 특성 SQL_FALSE;로 설정 된 경우 이러한 인수가 일반 인수로 처리 됩니다. 로 간주 됩니다 식별자 인수 대신이 특성은 SQL_TRUE로 설정 된 경우.  
  
 함수는 SQL_ERROR 및 SQLSTATE HY009 반환는 일반 인수를 null 포인터로 설정 하는 경우 인수는 필수 인수 (null 포인터를 잘못 사용). 일반 인수를 null 포인터로 설정 하는 경우 인수는 필수 인수가 아닙니다. 인수 동작은 드라이버에 따라 다릅니다. 필수 인수는 다음 표에 나열 됩니다.  
  
|함수|필수 인수|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|

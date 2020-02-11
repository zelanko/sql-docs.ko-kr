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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987823"
---
# <a name="ordinary-arguments"></a>일반 인수
카탈로그 함수 문자열 인수가 일반 인수인 경우 리터럴 문자열로 취급 됩니다. 일반 인수는 문자열 검색 패턴 또는 값 목록도 허용 하지 않습니다. 일반 인수의 경우는 의미가 있으며 문자열의 따옴표 문자는 문자 그대로 사용 됩니다. 이러한 인수는 SQL_ATTR_METADATA_ID statement 특성이 SQL_FALSE으로 설정 된 경우 일반 인수로 처리 됩니다. 이 특성이 SQL_TRUE로 설정 된 경우 대신 식별자 인수로 처리 됩니다.  
  
 일반 인수를 null 포인터로 설정 하 고 인수가 필수 인수 이면 함수는 SQL_ERROR 및 SQLSTATE HY009 (null 포인터를 잘못 사용 함)를 반환 합니다. 일반 인수가 null 포인터로 설정 되어 있고 인수가 필수 인수가 아니면 인수의 동작은 드라이버에 따라 달라 집니다. 다음 표에는 필수 인수가 나와 있습니다.  
  
|함수|필수 인수|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*Pktablename*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|

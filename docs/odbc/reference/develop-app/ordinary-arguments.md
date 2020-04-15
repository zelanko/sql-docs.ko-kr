---
title: 일반 인수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97362f93e91ccd8b592b4c05a0714b7602c1ba94
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282470"
---
# <a name="ordinary-arguments"></a>일반 인수
카탈로그 함수 문자열 인수가 일반 인수인 경우 리터럴 문자열로 처리됩니다. 일반 인수는 문자열 검색 패턴이나 값 목록을 허용하지 않습니다. 일반 인수의 경우는 중요하며 문자열의 따옴표 문자는 문자 그대로 수행됩니다. 이러한 인수는 SQL_ATTR_METADATA_ID 문 특성이 SQL_FALSE 설정된 경우 일반 인수로 처리됩니다. 이 특성이 SQL_TRUE 설정된 경우 식별자 인수로 처리됩니다.  
  
 일반 인수가 null 포인터로 설정되고 인수가 필수 인수인 경우 함수는 SQL_ERROR 및 SQLSTATE HY009(null 포인터의 잘못된 사용)를 반환합니다. 일반 인수가 null 포인터로 설정되어 있고 인수가 필수 인수가 아닌 경우 인수의 동작은 드라이버에 따라 다릅니다. 필요한 인수는 다음 표에 나열됩니다.  
  
|함수|필수 인수|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*Tablename*|  
|**SQLForeignKeys**|*PKTableName,* *FKTableName*|  
|**SQLPrimaryKeys**|*Tablename*|  
|**SQLSpecialColumns**|*Tablename*|  
|**SQLStatistics**|*Tablename*|

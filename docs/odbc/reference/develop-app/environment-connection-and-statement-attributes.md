---
title: 환경, 연결 및 명령문 특성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86cecaf0b82c7b6d15b3f37262507d2cff0c3c10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300933"
---
# <a name="environment-connection-and-statement-attributes"></a>환경, 연결 및 명령문 특성
ODBC는 환경, 연결 또는 명령문과 연결된 여러 특성을 정의합니다.  
  
 환경 특성은 연결 풀링이 활성화되어 있는지 여부와 같은 전체 환경에 영향을 미칩니다. 환경 특성은 **SQLSetEnvAttr로** 설정되고 **SQLGetEnvAttr로**검색됩니다.  
  
 연결 특성은 드라이버가 타이밍을 정하기 전에 데이터 원본에 연결하는 동안 기다려야 하는 시간 등 각 연결에 개별적으로 영향을 미칩니다. 연결 특성은 **SQLSetConnectAttr로** 설정되고 **SQLGetConnectAttr로**검색됩니다. 연결 특성에 대한 자세한 내용은 [연결 특성 을](../../../odbc/reference/develop-app/connection-attributes.md)참조하십시오.  
  
 문 특성은 문을 비동기적으로 실행해야 하는지 여부와 같이 각 문에 개별적으로 영향을 미칩니다. 명령문 특성은 **SQLSetStmtAttr로** 설정되고 **SQLGetStmtAttr로**검색됩니다. 몇 가지 문 특성은 읽기 전용 특성이며 설정할 수 없습니다. 예를 들어 커서의 현재 행 수를 검색하는 데 사용되는 SQL_ATTR_ROW_NUMBER 문 특성은 읽기 전용입니다. 명령문 특성에 대한 자세한 내용은 [명령문 특성 을](../../../odbc/reference/develop-app/statement-attributes.md)참조하십시오.  
  
 드라이버는 ODBC에 정의된 특성 외에도 자체 연결 및 문 특성을 정의할 수 있습니다. 드라이버 정의 특성은 Open Group에 등록되어 두 드라이버 공급업체가 동일한 정수 값을 다른 독점 특성에 할당하지 않도록 해야 합니다. 자세한 내용은 [드라이버 관련 데이터 유형, 설명자 유형, 정보 유형, 진단 유형 및 특성을](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)참조하십시오.  
  
 전체 특성 목록은 [SQLSetEnvAttr,](../../../odbc/reference/syntax/sqlsetenvattr-function.md) [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)및 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)을 참조하십시오. 대부분의 특성은 영향을 주는 ODBC 함수의 설명에도 설명되어 있습니다.

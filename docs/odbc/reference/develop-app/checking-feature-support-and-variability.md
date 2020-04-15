---
title: 기능 지원 및 가변성 확인 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47f16160c05d1c410e3889f0bb857befe88df5b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299173"
---
# <a name="checking-feature-support-and-variability"></a>기능 지원 및 가변성 확인
기능 지원 및 가변성을 확인하려면 응용 프로그램은 일반적으로 **SQLGetInfo,** **SQLGetFunctions**및 **SQLGetTypeInfo**를 호출합니다. 드라이버의 API 및 SQL 문법 적합성 수준이 좋은 시작 입니다. 광범위한 기능 지원에 대해 설명합니다. 그런 다음 응용 프로그램은 다른 옵션으로 **SQLGetInfo를** 호출하여 필요한 기능의 지원 또는 가변성을 결정하고, 반환된 준수 수준을 초과하는 함수가 지원되는지 여부를 결정하는 **SQLGetFunctions** 및 **SQLGetTypeInfo를** 사용하여 지원되는 SQL 데이터 형식을 결정할 수 있습니다.  
  
 응용 프로그램은 해당 특성을 사용하여 **SQLSetStmtAttr** 또는 **SQLSetConnectAttr을** 호출하여 명령문 또는 연결 특성이 지원되는지 여부를 결정할 수 있습니다. 함수가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환하면 특성이 지원됩니다. SQL_ERROR 및 SQLSTATE HYC00(선택적 기능이 구현되지 않음)을 반환하는 경우 특성이 지원되지 않습니다.  
  
 응용 프로그램은 **SQLDriver**를 호출하여 드라이버에 연결하기 전에 제한된 양의 정보를 결정할 수도 있습니다.

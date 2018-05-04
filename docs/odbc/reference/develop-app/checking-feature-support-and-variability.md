---
title: 기능 지원 및 변경 사항 확인 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2dfea013336a98ab4e69adf79198692e336acfd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="checking-feature-support-and-variability"></a>기능 지원 및 변경 사항 확인
기능 지원 및 가변성을 확인 하려면 응용 프로그램 일반적으로 호출 **SQLGetInfo**, **SQLGetFunctions**, 및 **SQLGetTypeInfo**합니다. 좋은 시작 지점은 드라이버의 API 및 SQL 문법 규칙 수준입니다. 이러한 광범위 한 수준의 기능 지원 설명합니다. 응용 프로그램이 호출할 수 **SQLGetInfo** 지원 또는 필요한 기능의 가변성을 결정 하는 다른 옵션과 **SQLGetFunctions** 확인 하려면 여부는 반환 된 다음 필요한 함수 규칙 수준, 사용할 수 및 **SQLGetTypeInfo** 를 어떤 SQL 데이터 형식이 지원 되는지 확인 합니다.  
  
 응용 프로그램은 문 또는 연결 특성 호출 하 여 사용할 수 있는지 여부를 결정할 수 **SQLSetStmtAttr** 또는 **SQLSetConnectAttr** 해당 특성입니다. 함수는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 특성은 지원 됩니다. SQLSTATE HYC00 및 SQL_ERROR를 반환 하는 경우 (선택적 기능이 구현 되지 않았습니다)는 특성이 지원 되지 않습니다.  
  
 응용 프로그램 제한 된 양의 정보를 호출 하 여 드라이버에 연결 하기 전에 확인할 수도 **SQLDrivers**합니다.

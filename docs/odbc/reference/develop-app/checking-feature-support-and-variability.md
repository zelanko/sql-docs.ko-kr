---
title: 기능 지원 및 가변성 확인 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 21495e538a554a477336d1a92926c11fe762c5af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062659"
---
# <a name="checking-feature-support-and-variability"></a>기능 지원 및 가변성 확인
기능 지원 및 가변성을 확인 하려면 응용 프로그램 일반적으로 호출 **SQLGetInfo**하십시오 **SQLGetFunctions**, 및 **SQLGetTypeInfo**합니다. 시작에 좋은 위치는 드라이버의 API 및 SQL 문법 규칙 수준입니다. 이러한 광범위 한 수준의 기능 지원 설명합니다. 응용 프로그램을 호출할 수 있습니다 **SQLGetInfo** 가변성에 필요한 기능을 지원 하는 다른 옵션을 사용 하 여 **SQLGetFunctions** 결정할 여부 반환 된 초과 해야 함수 규칙 수준 지원 하 고 **SQLGetTypeInfo** 지 원하는 SQL 데이터 형식을 확인 하려면.  
  
 응용 프로그램은 문 또는 연결 특성을 호출 하 여 지원 되는지 여부를 확인할 수 있습니다 **SQLSetStmtAttr** 하거나 **SQLSetConnectAttr** 해당 특성을 사용 하 여 합니다. 함수는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 특성은 지원 됩니다. SQLSTATE HYC00 및 SQL_ERROR를 반환 하는 경우 (선택적 기능 구현 되지 않음)에 특성이 지원 되지 않습니다.  
  
 응용 프로그램을 제한 된 양의 호출 하 여 드라이버에 연결 하기 전에 정보를 확인할 수도 있습니다 **SQLDrivers**합니다.

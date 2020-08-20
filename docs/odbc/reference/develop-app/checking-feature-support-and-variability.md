---
description: 기능 지원 및 가변성 확인
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60fb6b39d7b2326a925aea40303ce52165cca8a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465915"
---
# <a name="checking-feature-support-and-variability"></a>기능 지원 및 가변성 확인
기능 지원 및 가변성을 확인 하기 위해 응용 프로그램은 일반적으로 **SQLGetInfo**, **SQLGetFunctions**및 **SQLGetTypeInfo**를 호출 합니다. 좋은 출발점은 드라이버의 API 및 SQL 문법 규칙 수준입니다. 이는 광범위 한 기능 지원 수준에 대해 설명 합니다. 그런 다음 응용 프로그램은 다른 옵션을 사용 하 여 **SQLGetInfo** 를 호출 하 여 필요한 기능의 지원 또는 산포도를 결정 하 고, 반환 된 규칙 수준을 **초과 하는** 함수가 지원 되는지 여부를 결정 하 고, **SQLGETFUNCTIONS** 에서 지원 되는 SQL 데이터 형식을 확인할 수 있습니다.  
  
 응용 프로그램은 해당 특성과 함께 **SQLSetStmtAttr** 또는 **SQLSetConnectAttr** 를 호출 하 여 문 또는 연결 특성이 지원 되는지 여부를 결정할 수 있습니다. 함수가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 특성이 지원 됩니다. SQL_ERROR 및 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)를 반환 하는 경우이 특성은 지원 되지 않습니다.  
  
 응용 프로그램은 **Sqldrivers**를 호출 하 여 드라이버에 연결 하기 전에 제한 된 양의 정보를 확인할 수도 있습니다.

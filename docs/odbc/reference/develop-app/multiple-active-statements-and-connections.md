---
description: 다중 활성 문 및 연결
title: 여러 활성 문 및 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56897dedbd1bf0d96dfa73f75a28db5f1ca46c43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429265"
---
# <a name="multiple-active-statements-and-connections"></a>다중 활성 문 및 연결
일부 드라이버와 Dbms에서는 한 번에 활성화 될 수 있는 문과 연결의 수를 제한 합니다. 이러한 숫자는 1 보다 작을 수 있습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명의 SQL_MAX_CONCURRENT_ACTIVITIES 및 SQL_MAX_DRIVER_CONNECTIONS 옵션과 [문 핸들](../../../odbc/reference/develop-app/statement-handles.md) 및 [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)을 참조 하십시오.

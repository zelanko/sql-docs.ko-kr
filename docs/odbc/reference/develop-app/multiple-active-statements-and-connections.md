---
title: "여러 활성 문 및 연결 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17be494898610bffba590548767a9d7c3e2915f8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="multiple-active-statements-and-connections"></a>여러 활성 문 및 연결
일부 드라이버 및 Dbms 문 및 한 번에 활성화 될 수 있는 연결 수를 제한 합니다. 이 숫자 하나로 작을 수 있습니다. 자세한 내용은의 SQL_MAX_CONCURRENT_ACTIVITIES 및 SQL_MAX_DRIVER_CONNECTIONS 옵션을 참조 하십시오.는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명, 및 [문은 처리](../../../odbc/reference/develop-app/statement-handles.md) 및 [ 연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)합니다.

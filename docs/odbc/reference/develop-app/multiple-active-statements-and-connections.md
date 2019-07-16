---
title: 다중 활성 문 및 연결 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76b74ff748a62a401955e4ea4a995f507314124e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942822"
---
# <a name="multiple-active-statements-and-connections"></a>다중 활성 문 및 연결
일부 드라이버 및 Dbms 문 및 한 번에 활성화 될 수 있는 연결 수를 제한 합니다. 이러한 숫자 하나로 작게 만들 수 있습니다. 자세한 내용은 SQL_MAX_CONCURRENT_ACTIVITIES 및 SQL_MAX_DRIVER_CONNECTIONS 옵션을 참조 하세요. 합니다 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명, 및 [문은 처리](../../../odbc/reference/develop-app/statement-handles.md) 및 [ 연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)합니다.

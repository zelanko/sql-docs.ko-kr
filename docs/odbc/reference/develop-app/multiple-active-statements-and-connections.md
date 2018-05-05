---
title: 여러 활성 문 및 연결 | Microsoft Docs
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
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b548b6d1b1aa7e7b260abcc9f507e2dbd566e7c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="multiple-active-statements-and-connections"></a>여러 활성 문 및 연결
일부 드라이버 및 Dbms 문 및 한 번에 활성화 될 수 있는 연결 수를 제한 합니다. 이 숫자 하나로 작을 수 있습니다. 자세한 내용은의 SQL_MAX_CONCURRENT_ACTIVITIES 및 SQL_MAX_DRIVER_CONNECTIONS 옵션을 참조 하십시오.는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명, 및 [문은 처리](../../../odbc/reference/develop-app/statement-handles.md) 및 [ 연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)합니다.

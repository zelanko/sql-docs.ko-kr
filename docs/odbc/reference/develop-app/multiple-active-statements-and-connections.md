---
title: 여러 활성 문 및 연결 | 마이크로 소프트 문서
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
ms.openlocfilehash: 8259967942f47b06c50a9043158f8b3b45c58d7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302432"
---
# <a name="multiple-active-statements-and-connections"></a>다중 활성 문 및 연결
일부 드라이버 및 DBMS는 한 번에 활성화할 수 있는 명령문 및 연결 수를 제한합니다. 이 숫자는 하나만큼 작을 수 있습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명및 [명령문 핸들](../../../odbc/reference/develop-app/statement-handles.md) 및 [연결 핸들의](../../../odbc/reference/develop-app/connection-handles.md)SQL_MAX_CONCURRENT_ACTIVITIES 및 SQL_MAX_DRIVER_CONNECTIONS 옵션을 참조하십시오.

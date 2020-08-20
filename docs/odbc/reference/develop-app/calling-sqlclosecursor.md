---
description: SQLCloseCursor 호출
title: SQLCloseCursor 호출 Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 925617d79266f0b50ef9b38586b31af91311b63e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494773"
---
# <a name="calling-sqlclosecursor"></a>SQLCloseCursor 호출
**SQLCloseCursor** 는 SQL_CLOSE **SQLFreeStmt** 와 거의 동일 하므로 드라이버 관리자는이 함수를 매핑하지 않습니다. 기존 ODBC *2.x 응용 프로그램이* 새 함수를 *사용 하 여 odbc 2.x* 로 쉽게 이동할 수 있도록 대체 함수가 매핑됩니다. 이러한 이동을 통해 이러한 응용 프로그램은 모듈식 방식으로 조건부 코드 내에서 *새로운 ODBC 3.x* 기능을 보다 쉽게 사용할 수 있습니다. **SQLCloseCursor** 는 새로운 기능을 나타내지 않습니다. 응용 프로그램은 SQL_CLOSE를 사용 하 여 **SQLFreeStmt** 에서 **SQLCloseCursor** 로 이동 하 여 이점을 얻을 수 없습니다.

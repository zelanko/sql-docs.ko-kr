---
title: SQLCloseCursor 호출 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da5a674f86228c71a26e621936dc711a688a684d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793937"
---
# <a name="calling-sqlclosecursor"></a>SQLCloseCursor 호출
때문에 **SQLCloseCursor** 거의 동일 **SQLFreeStmt** SQL_CLOSE를 사용 하 여 드라이버 관리자는이 함수 매핑되지 않습니다. 대체 함수는 기존 있도록 매핑됩니다 ODBC *2.x* 응용 프로그램을 ODBC 쉽게 이동할 수 있습니다 *3.x* 새 함수를 사용 하 여 합니다. 이러한 이동 쉽게 새 ODBC를 사용 하려면 이러한 응용 프로그램에 대 한 *3.x* 모듈식에서 조건부 코드 내에서 기능입니다. **SQLCloseCursor** 모든 새 기능을 나타내지 않습니다. 응용 프로그램으로 이동 하 여 모든 이점은 얻지 **SQLCloseCursor** 에서 **SQLFreeStmt** SQL_CLOSE를 사용 하 여 합니다.

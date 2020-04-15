---
title: SQLCloseCursor 호출 | 마이크로 소프트 문서
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
ms.openlocfilehash: 2feab58de28e39747a1d9c819f9f15426b156151
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306276"
---
# <a name="calling-sqlclosecursor"></a>SQLCloseCursor 호출
**SQLCloseCursor는** SQL_CLOSE **SQLFreeStmt와** 거의 동일하므로 드라이버 관리자는 이 함수를 매핑하지 않습니다. 교체 함수는 기존 ODBC *2.x* 응용 프로그램이 새 기능을 사용하여 ODBC *3.x로* 쉽게 이동할 수 있도록 매핑됩니다. 이러한 이동을 통해 이러한 응용 프로그램은 모듈식 방식으로 조건부 코드 내부에서 새로운 ODBC *3.x* 기능을 사용하기 쉽게 시작할 수 있습니다. **SQLCloseCursor는** 새 기능을 나타내지 않습니다. 응용 프로그램은 SQL_CLOSE **SQLFreeStmt에서** **SQLCloseCursor로** 이동하여 이점을 얻지 못합니다.

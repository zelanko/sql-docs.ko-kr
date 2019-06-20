---
title: SQLGetDiagField 호출 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a27584a0892bc468b50286b79edbe92d7c968a0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199150"
---
# <a name="calling-sqlgetdiagfield"></a>SQLGetDiagField 호출
때 ODBC 3. *x* 응용 프로그램 호출 **SQLGetDiagField** 는 ODBC 2 *.x* 드라이버를 드라이버에서 반환의 적절 한 정보와 관계 없이 SQL_SUCCESS  *\*DiagInfoPtr* 경우는 *DiagIdentifier* 인수가 SQL_DIAG_CLASS_ORIGIN SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_ 숫자, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME, 또는 SQL_DIAG_SQLSTATE 합니다. 다른 모든 진단 필드에서 SQL_ERROR를 반환 합니다.

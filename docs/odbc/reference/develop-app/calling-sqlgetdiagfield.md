---
title: "SQLGetDiagField를 호출 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2661b39babaea276e41f04f532c0d4b94d59259
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="calling-sqlgetdiagfield"></a>SQLGetDiagField를 호출합니다.
때 ODBC 3. *x* 응용 프로그램 호출 **SQLGetDiagField** ODBC 2에서*.x* 드라이버를 드라이버에서는 반환의 적절 한 정보와 SQL_SUCCESS  *\*DiagInfoPtr* 경우는 *DiagIdentifier* SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_ 인수는 숫자, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME, 또는 SQL_DIAG_SQLSTATE 합니다. 다른 모든 진단 필드는 SQL_ERROR를 반환 합니다.

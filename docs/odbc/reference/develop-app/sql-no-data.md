---
title: SQL_NO_DATA | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299793"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
때 ODBC 3. *x* 응용 프로그램은 **SQLExecDirect,** **SQLExecute**또는 **SQLParamData를** ODBC 2에서 호출합니다. *x* 드라이버는 데이터 원본의 행에 영향을 주지 않는 검색된 업데이트를 실행하거나 문을 삭제하려면 드라이버가 SQL_NO_DATA SQL_SUCCESS 반환해야 합니다. 때 ODBC 2. *x* 또는 ODBC 3. *x* 응용 프로그램은 ODBC 3로 작업합니다. *x* 드라이버는 **SQLExecDirect,** **SQLExecute**또는 **SQLParamData와** 동일한 결과, ODBC 3을 호출합니다. *x* 드라이버는 SQL_NO_DATA 반환해야합니다.

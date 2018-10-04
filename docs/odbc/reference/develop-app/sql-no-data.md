---
title: SQL_NO_DATA | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 749351694a41764b9b5cc8bf3421340d62626aaf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47739891"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
때 ODBC 3. *x* 응용 프로그램 호출 **SQLExecDirect**에 **SQLExecute**, 또는 **SQLParamData** 에 ODBC 2. *x* 드라이버를 검색 결과 업데이트를 실행 하거나 데이터 원본 드라이버에서 모든 행에 영향을 미치지 않는 문을 삭제 되지 SQL_NO_DATA 관계 없이 SQL_SUCCESS를 반환 해야 합니다. 경우는 ODBC 2. *x* 또는 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 3. *x* 드라이버 호출 **SQLExecDirect**를 **SQLExecute**, 또는 **SQLParamData** 여 동일한 결과 ODBC 3. *x* 드라이버에서 SQL_NO_DATA를 반환 해야 합니다.

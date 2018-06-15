---
title: SQL_NO_DATA | Microsoft Docs
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
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff7ba5184642f419a62ffef0610bfc08995ed6b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911218"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
때 ODBC 3. *x* 응용 프로그램 호출 **SQLExecDirect**, **SQLExecute**, 또는 **SQLParamData** ODBC 2에서. *x* 드라이버 데이터 소스의 모든 행에 영향을 미치지 않는 문을 삭제 하거나 검색 결과 업데이트를 실행 하는 드라이버 하지 SQL_NO_DATA 관계 없이 SQL_SUCCESS를 반환 해야 합니다. 경우는 ODBC 2. *x* 또는 ODBC 3. *x* 응용 프로그램을 사용 하는 ODBC 3. *x* 드라이버 호출 **SQLExecDirect**, **SQLExecute**, 또는 **SQLParamData** 와 동일한 결과 ODBC 3. *x* 드라이버는 SQL_NO_DATA를 반환 해야 합니다.

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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299793"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
ODBC 3 인 경우 *x* 응용 프로그램은 ODBC 2에서 **sqlexecdirect**, **Sqlexecute**또는 **sqlexecdirect** 를 호출 합니다. *x* 드라이버 데이터 원본의 행에 영향을 주지 않는 검색 된 update 또는 delete 문을 실행 하려면 드라이버가 SQL_NO_DATA 아닌 SQL_SUCCESS을 반환 해야 합니다. ODBC 2 인 경우 *x* 또는 ODBC 3. ODBC 3에서 작동 하는 *x* 응용 프로그램입니다. *x* 드라이버는 동일한 결과 (ODBC 3)를 사용 하 여 **sqlexecdirect**, **Sqlexecute**또는 **sqlexecdirect** 를 호출 합니다. *x* 드라이버는 SQL_NO_DATA을 반환 해야 합니다.

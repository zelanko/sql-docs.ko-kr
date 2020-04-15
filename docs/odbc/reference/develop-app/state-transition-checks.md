---
title: 상태 전환 검사 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dc1ddc126a2d652dfdb038cbb0e510f9735d7b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299708"
---
# <a name="state-transition-checks"></a>상태 전환 검사
드라이버 관리자는 환경, 연결 또는 명령문의 상태가 호출되는 함수에 적합한지 확인합니다. 예를 들어 **SQLConnect가** 호출될 때 연결이 할당된 상태여야 합니다. **SQLExecute가** 호출될 때 문은 준비된 상태여야 합니다. 드라이버 관리자는 상태 전환 오류에 대해 SQL_ERROR 반환합니다.

---
title: 상태 전환 검사 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b337d317092ad6ae20cc91236d69c1314de96bce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107279"
---
# <a name="state-transition-checks"></a>상태 전환 검사
드라이버 관리자는 환경, 연결 또는 문의 상태가 호출 되는 함수에 적합 한지 확인 합니다. 예를 들어 **SQLConnect** 가 호출 되 면 연결이 할당 된 상태 여야 합니다. 문은 **Sqlexecute** 를 호출할 때 준비 된 상태 여야 합니다. 드라이버 관리자는 상태 전환 오류에 대 한 SQL_ERROR를 반환 합니다.

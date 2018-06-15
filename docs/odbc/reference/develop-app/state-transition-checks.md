---
title: 상태 전환 검사 | Microsoft Docs
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
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23f2b87fc943535075e1456bb31366ff9667b07b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910628"
---
# <a name="state-transition-checks"></a>상태 전환 검사
드라이버 관리자의 환경, 연결 또는 문이 상태 호출 함수에 대 한 적절 한 하는지 확인 합니다. 예를 들어 한 연결 이어야 합니다는 할당 된 상태의 **SQLConnect** 가 호출 되는 문 준비에 있어야 하면 상태로 **SQLExecute** 호출 됩니다. 드라이버 관리자는 상태 전환 오류에 대 한 SQL_ERROR를 반환합니다.

---
title: "상태 전환 검사 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a6873114b5d15bdf9bfbac369dacaea712a0236
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="state-transition-checks"></a>상태 전환 검사
드라이버 관리자의 환경, 연결 또는 문이 상태 호출 함수에 대 한 적절 한 하는지 확인 합니다. 예를 들어 한 연결 이어야 합니다는 할당 된 상태의 **SQLConnect** 가 호출 되는 문 준비에 있어야 하면 상태로 **SQLExecute** 호출 됩니다. 드라이버 관리자는 상태 전환 오류에 대 한 SQL_ERROR를 반환합니다.


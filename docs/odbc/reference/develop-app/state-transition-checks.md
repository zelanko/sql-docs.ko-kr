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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107279"
---
# <a name="state-transition-checks"></a>상태 전환 검사
드라이버 관리자 환경, 연결 또는 문이 상태의 호출 함수에 대 한 적절 한 인지를 확인 합니다. 예를 들어 연결 이어야 합니다는 할당 된 상태의 **SQLConnect** 가 호출 되는 문 준비에 있어야 합니다. 상태의 **SQLExecute** 라고 합니다. 드라이버 관리자 상태 전환 오류에 대 한 SQL_ERROR를 반환합니다.

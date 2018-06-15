---
title: 드라이버 관리자 진단 예 | Microsoft Docs
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
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c383dda247d3309ed38744609afb5ca12e3c38f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909208"
---
# <a name="driver-manager-diagnostic-example"></a>드라이버 관리자 진단 예제
드라이버 관리자는 진단 메시지를 생성할 수도 수 있습니다. 예를 들어, 응용 프로그램에 잘못 된 방향 옵션을 전달 하는 경우 **SQLDataSources**, 드라이버 관리자 형식과 다음 값이 반환 될 수 있습니다 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 드라이버 관리자에서이 오류가 발생 하기 때문에 있으므로 접두사에 추가 진단 메시지 ([Microsoft]) 공급 업체 및 해당 식별자 ([ODBC 드라이버 관리자])에 대 한 합니다.

---
title: 드라이버 관리자 진단 예제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ad253c2d0603846d6d1f795f6115e7bb727b3da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238045"
---
# <a name="driver-manager-diagnostic-example"></a>드라이버 관리자 진단 예제
드라이버 관리자 진단 메시지를 생성할 수도 있습니다. 예를 들어, 응용 프로그램에 잘못 된 방향 옵션을 전달 하는 경우 **SQLDataSources**, 드라이버 관리자 형식과에서 같은 값을 반환할 수 있습니다 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 을 드라이버 관리자에서 오류가 발생 하기 때문에 접두사에 추가 진단 메시지 해당 공급 업체 ([Microsoft]) 및 해당 식별자 ([ODBC 드라이버 관리자])에 대 한 합니다.

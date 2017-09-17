---
title: "드라이버 관리자 진단 예 | Microsoft Docs"
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
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3f373fe012c2b791329fea35ca853021e70274eb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-diagnostic-example"></a>드라이버 관리자 진단 예제
드라이버 관리자는 진단 메시지를 생성할 수도 수 있습니다. 예를 들어, 응용 프로그램에 잘못 된 방향 옵션을 전달 하는 경우 **SQLDataSources**, 드라이버 관리자 형식과 다음 값이 반환 될 수 있습니다 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 드라이버 관리자에서이 오류가 발생 하기 때문에 있으므로 접두사에 추가 진단 메시지 ([Microsoft]) 공급 업체 및 해당 식별자 ([ODBC 드라이버 관리자])에 대 한 합니다.

---
title: 드라이버 관리자 진단 예제 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 839095e5544cab73cdddd4f4b17a3d8d52136c9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305814"
---
# <a name="driver-manager-diagnostic-example"></a>드라이버 관리자 진단 예제
드라이버 관리자는 진단 메시지를 생성할 수도 있습니다. 예를 들어 응용 프로그램이 잘못된 방향 옵션을 **SQLDataSource에**전달한 경우 드라이버 관리자는 **SQLGetDiagRec에서**다음 값을 서식을 지정하고 반환할 수 있습니다.  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 드라이버 관리자에서 오류가 발생했기 때문에 공급업체([Microsoft]))와 해당 식별자([ODBC 드라이버 관리자])에 대한 진단 메시지에 접두사를 추가했습니다.

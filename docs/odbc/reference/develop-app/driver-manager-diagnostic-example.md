---
title: 드라이버 관리자 진단 예 | Microsoft Docs
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
ms.openlocfilehash: 95392367b70af3eb820f0943af5dc668783a3fe5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046965"
---
# <a name="driver-manager-diagnostic-example"></a>드라이버 관리자 진단 예제
또한 드라이버 관리자는 진단 메시지를 생성할 수 있습니다. 예를 들어 응용 프로그램이 **Sqldatasources 원본**에 잘못 된 방향 옵션을 전달한 경우 드라이버 관리자는 **SQLGetDiagRec**에서 다음 값을 포맷 하 고 반환할 수 있습니다.  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 드라이버 관리자에서 오류가 발생 했기 때문에 해당 공급 업체 ([Microsoft]) 및 해당 식별자 ([ODBC 드라이버 관리자])에 대 한 접두사를 진단 메시지에 추가 했습니다.

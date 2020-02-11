---
title: 파일 기반 드라이버 진단 예제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23234a490f664c4be0811152b2b77ae7c0b73761
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069828"
---
# <a name="file-based-driver-diagnostic-example"></a>파일 기반 드라이버 진단 예제
파일 기반 드라이버는 ODBC 드라이버와 데이터 원본으로 모두 작동 합니다. 따라서 ODBC 연결의 구성 요소 및 데이터 원본으로 오류와 경고를 생성할 수 있습니다. 또한 드라이버 관리자와 상호 작용 하는 구성 요소 이기 때문에 **SQLGetDiagRec**에 대 한 인수를 포맷 하 고 반환 합니다.  
  
 예를 들어, dBASE 용 Microsoft® 드라이버에서 충분 한 메모리를 할당할 수 없는 경우 **SQLGetDiagRec**에서 다음 값을 반환할 수 있습니다.  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 이 오류가 데이터 원본과 관련이 없기 때문에 드라이버는 공급 업체 ([Microsoft]) 및 드라이버 ([ODBC dBASE Driver])에 대 한 진단 메시지에만 접두사를 추가 했습니다.  
  
 드라이버가 Employee .dbf 파일을 찾을 수 없는 경우 **SQLGetDiagRec**에서 다음 값을 반환할 수 있습니다.  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 이 오류가 데이터 원본과 관련 되어 있으므로 드라이버는 데이터 원본 ([dBASE])의 파일 형식을 진단 메시지의 접두사로 추가 했습니다. 드라이버는 데이터 원본으로 되 하는 구성 요소 이기도 하므로 공급 업체 ([Microsoft]) 및 드라이버 ([ODBC dBASE Driver])에 대 한 접두사를 추가 했습니다.

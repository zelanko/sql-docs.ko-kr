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
manager: craigg
ms.openlocfilehash: decb09098cee4b9ab6473e3c622b9917a89e9b09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809321"
---
# <a name="file-based-driver-diagnostic-example"></a>파일 기반 드라이버 진단 예제
파일 기반 드라이버는 ODBC 드라이버 및 데이터 원본으로 작동합니다. 생성할 수 있습니다 따라서 오류 및 경고를 모두 구성 요소로 데이터 원본 및 ODBC 연결에서 합니다. 이기 때문에 드라이버 관리자와 인터페이스 하는 구성 요소 형식 및 인수에 대 한 반환 **SQLGetDiagRec**합니다.  
  
 예를 들어, dBASE Microsoft® 드라이버 충분 한 메모리를 할당할 수 없습니다, 하는 경우에서 다음 값을 반환할 수 있습니다 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 이 오류를 데이터 원본 관련이 없는, 때문에 드라이버만 접두사에 추가 진단 메시지 ([Microsoft]) 공급 업체 및 드라이버 ([ODBC dBASE 드라이버]).  
  
 드라이버 Employee.dbf 파일을 찾을 수 없습니다, 하는 경우에서 다음 값을 반환할 수 있습니다 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 이 오류는 데이터 원본에 관련 된, 드라이버 파일에 대 한 형식의 데이터 원본 ([dBASE]) 접두사로 진단 메시지 추가. 드라이버 데이터 원본과 되는 구성 요소 또한 되었으므로 ([Microsoft]) 공급 업체와 드라이버 ([ODBC dBASE 드라이버])에 대 한 접두사를 추가 합니다.

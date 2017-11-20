---
title: "파일 기반 드라이버 진단 예 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 309bea8c888b7fd057e942dd348125c9b420afb7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="file-based-driver-diagnostic-example"></a>파일 기반 드라이버 진단 예제
파일 기반 드라이버는 ODBC 드라이버 및 데이터 원본으로 사용 됩니다. ODBC 연결에 및 데이터 원본으로 오류 및 경고를 모두 구성 요소로 생성 따라서 것입니다. 이기 때문에 드라이버 관리자와 교류 하는 구성 요소 형식 및 인수에 대 한 반환 **SQLGetDiagRec**합니다.  
  
 예를 들어 dBASE Microsoft® 드라이버 충분 한 메모리를 할당할 수 없으므로, 하는 경우 다음 값에서 반환할 수 있습니다 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 이 오류는 데이터 소스에 연관성이, 때문에 드라이버만 접두사에 추가 진단 메시지 ([Microsoft]) 공급 업체 및 드라이버 ([ODBC dBASE 드라이버]).  
  
 다음 값을 반환할 수 있습니다 드라이버 Employee.dbf 파일을 찾을 수 없는, 경우 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 이 오류는 데이터 원본에 관련 된, 때문에 진단 메시지에 데이터 원본 ([dBASE])의 파일 형식을 접두사로 추가 드라이버. 드라이버 데이터 원본과 역시 하는 구성 요소 또한 되었으므로 접두사 ([Microsoft]) 공급 업체와 드라이버 ([ODBC dBASE 드라이버])에 대 한 추가 합니다.


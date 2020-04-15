---
title: 파일 기반 드라이버 진단 예제 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f09e4f4758b6276836b08f02b24fb31dd1fadc7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305641"
---
# <a name="file-based-driver-diagnostic-example"></a>파일 기반 드라이버 진단 예제
파일 기반 드라이버는 ODBC 드라이버와 데이터 원본 역할을 모두 합니다. 따라서 ODBC 연결의 구성 요소와 데이터 원본으로 오류 및 경고를 생성할 수 있습니다. 또한 드라이버 관리자와 인터페이스하는 구성 요소이기 때문에 **SQLGetDiagRec**에 대한 인수를 서식을 지정하고 반환합니다.  
  
 예를 들어 dBASE에 대한 Microsoft ® 드라이버가 충분한 메모리를 할당할 수 없는 경우 **SQLGetDiagRec에서**다음 값을 반환할 수 있습니다.  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 이 오류는 데이터 원본과 관련이 없기 때문에 드라이버는 공급업체([Microsoft]))와 드라이버([ODBC dBASE 드라이버])에 대한 진단 메시지에 접두사만 추가했습니다.  
  
 드라이버가 Employee.dbf 파일을 찾을 수 없는 경우 **SQLGetDiagRec에서**다음 값을 반환할 수 있습니다.  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 이 오류는 데이터 원본과 관련이 있기 때문에 드라이버는 데이터 원본의 파일 형식을 [dBASE]를 진단 메시지의 접두사로 추가했습니다. 드라이버는 데이터 원본과 인터페이스하는 구성 요소이기도 했기 때문에 공급업체([Microsoft]))와 드라이버([ODBC dBASE 드라이버])에 대한 접두사를 추가했습니다.

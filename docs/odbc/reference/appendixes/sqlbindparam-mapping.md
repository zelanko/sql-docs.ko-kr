---
title: SQLBindParam 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1df595722297c91dc75398470912188e109e278
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305443"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 매핑
**SQLBindParam은** ODBC에서 전혀 없었기 때문에 더 이상 호출할 수 없습니다. 그러나 여전히 중복된 기능을 나타내며 ISO 및 Open 그룹 호환 응용 프로그램이 이를 사용하기 때문에 드라이버 관리자는 내보내야 합니다. **SQLBindParameter** **SQLBindParam의**모든 기능을 포함 하기 때문에 **SQLBindParam** **SQLBindParameter** (기본 드라이버는 ODBC *3.x* 드라이버)의 상단에 매핑 됩니다. ODBC *3.x* 드라이버는 **SQLBindParam**을 구현할 필요가 없습니다.  
  
## <a name="remarks"></a>설명  
 **SQLBindParam에** 대한 다음 호출이 수행될 때:  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 드라이버 관리자는 다음과 같이 드라이버에서 **SQLBindParameter를** 호출합니다.  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 [64비트](../../../odbc/reference/odbc-64-bit-information.md)운영 체제에서 응용 프로그램이 실행되는 경우 ODBC 64비트 정보를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [사용되지 않는 함수와 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)

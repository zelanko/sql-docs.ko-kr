---
title: SQLBindParam 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a2c78cd97b6577be8d11d07325165d6d82cd895
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 매핑
**SQLBindParam** 진정으로 호출할 수 없습니다 사용 되지 않는 있는 ODBC 되지 않은; 하지만 중복 된 기능 여전히 나타냅니다-ISO 및 Open 그룹 – 호환 응용 프로그램은 사용 하기 때문에 내보낼 드라이버 관리자를 사용 해야 합니다. 때문에 **SQLBindParameter** 의 모든 기능을 포함 **SQLBindParam**, **SQLBindParam** 위쪽에 매핑할 수 **SQLBindParameter** (기본 드라이버는 ODBC 3 경우*.x* 드라이버). ODBC 3*.x* 드라이버를 구현 하지 않아도 **SQLBindParam**합니다.  
  
## <a name="remarks"></a>주의  
 다음을 호출 하는 경우 **SQLBindParam** 이루어집니다.  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 드라이버 관리자를 호출 하 여 **SQLBindParameter** 다음과 같이 드라이버에서:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 참조 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우.  
  
## <a name="see-also"></a>관련 항목:  
 [사용되지 않는 함수와 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)

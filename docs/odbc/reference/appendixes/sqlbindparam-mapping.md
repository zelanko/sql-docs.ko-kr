---
title: SQLBindParam 매핑 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57e0fe66d76f91c8cea35710e9d0245db7619628
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544430"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 매핑
**SQLBindParam** 진정으로 호출할 수 없습니다 사용 되지 않는 되지 않아 있습니다 odbc; 그러나 여전히 나타내므로 중복 된 기능-드라이버 관리자가 ISO 및 열린 그룹 호환 응용 프로그램은 사용 하기 때문에 내보내기 해야 합니다. 때문에 **SQLBindParameter** 의 모든 기능을 포함 **SQLBindParam**하십시오 **SQLBindParam** 위쪽에 매핑될 **SQLBindParameter** (기본 드라이버는 ODBC 3 경우 *.x* 드라이버). ODBC 3 *.x* 드라이버를 구현할 필요가 없습니다 **SQLBindParam**합니다.  
  
## <a name="remarks"></a>Remarks  
 다음을 호출 하는 경우 **SQLBindParam** 이루어집니다.  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 드라이버 관리자 호출 **SQLBindParameter** 같이 드라이버에서:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 참조 [ODBC 64-Bit 정보](../../../odbc/reference/odbc-64-bit-information.md)이면 응용 프로그램을 64 비트 운영 체제에서 실행 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용되지 않는 함수와 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)

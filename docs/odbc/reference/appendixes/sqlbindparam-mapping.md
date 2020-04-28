---
title: Sqlbindparam 함수와 매핑 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305443"
---
# <a name="sqlbindparam-mapping"></a>SQLBindParam 매핑
**Sqlbindparam 함수와** 는 ODBC에 없기 때문에 실제로는 사용 되지 않는 것으로 호출할 수 없습니다. 그러나 여전히 중복 된 기능을 나타냅니다. ISO 및 오픈 그룹 규격 응용 프로그램에서이 기능을 사용 하기 때문에 드라이버 관리자가 내보내야 합니다. **SQLBindParameter** 에는 **sqlbindparam 함수와**의 모든 기능이 포함 되어 있기 때문에 **sqlbindparam 함수와** 는 **SQLBindParameter** 의 맨 위에 매핑됩니다 (기본 *드라이버가 ODBC 3.x* 드라이버 인 경우). ODBC 3.x 드라이버는 **sqlbindparam 함수와**를 구현할 필요가 *없습니다.*  
  
## <a name="remarks"></a>설명  
 **Sqlbindparam 함수와** 에 대 한 다음 호출이 수행 될 때:  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 드라이버 관리자는 드라이버에서 다음과 같이 **SQLBindParameter** 를 호출 합니다.  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 응용 프로그램이 64 비트 운영 체제에서 실행 되는 경우 [ODBC 64 비트 정보](../../../odbc/reference/odbc-64-bit-information.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [사용되지 않는 함수와 매핑](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)

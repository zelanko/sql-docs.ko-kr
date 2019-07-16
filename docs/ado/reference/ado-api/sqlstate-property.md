---
title: SQLState 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e43ace17f3f2b709c327f185a189a107b6b73065
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916879"
---
# <a name="sqlstate-property"></a>SQLState 속성
SQL 상태를 나타냅니다는 주어진 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 5 자로 이루어진 반환 **문자열** ANSI SQL 표준을 따르는 및 오류 코드를 표시 하는 값입니다.  
  
## <a name="remarks"></a>설명  
 사용 된 **SQLState** SQL 문 처리 하는 동안 오류가 발생 하는 경우 공급자를 반환 하는 5 문자 오류 코드를 읽을 속성입니다. 예를 들어, Microsoft OLE DB Provider for ODBC와 함께 사용할 경우 Microsoft SQL Server 데이터베이스를 SQL 상태 오류 코드에서에서 발생 ODBC, ODBC에 고유한 오류 또는 Microsoft SQL Server에서 시작 되며 다음 ODBC에 매핑되는 오류를 기반으로 오류가 발생 했습니다. 이러한 오류 코드는 ANSI SQL 표준에 설명 되어 있습니다 하지만 다른 데이터 원본에 의해 다르게 구현 될 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, HelpFile, NativeError, 번호, 원본 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   

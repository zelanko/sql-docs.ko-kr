---
description: SQLState 속성
title: SQLState 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bbc849f19c91f7b2387df5e0e71b3455efa0db09
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988864"
---
# <a name="sqlstate-property"></a>SQLState 속성
지정 된 [오류](./error-object.md) 개체에 대 한 SQL 상태를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 ANSI SQL 표준에 따라 5 자리 **문자열** 값을 반환 하 고 오류 코드를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 **SQLState** 속성을 사용 하 여 SQL 문을 처리 하는 동안 오류가 발생할 때 공급자가 반환 하는 5 문자 오류 코드를 읽을 수 있습니다. 예를 들어 Microsoft SQL Server 데이터베이스와 함께 ODBC 용 Microsoft OLE DB 공급자를 사용 하는 경우 SQL 상태 오류 코드는 odbc와 관련 된 오류 또는 Microsoft SQL Server에서 발생 하는 오류에 따라 ODBC에서 시작 된 다음 ODBC 오류에 매핑됩니다. 이러한 오류 코드는 ANSI SQL 표준에 설명 되어 있지만 다른 데이터 소스에 따라 다르게 구현 될 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](./error-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)
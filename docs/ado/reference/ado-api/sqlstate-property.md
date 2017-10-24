---
title: "SQLState 속성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f65624cc9393a1ce676530102d41eb1655bcf79b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlstate-property"></a>SQLState 속성
SQL 상태를 나타냅니다는 주어진 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 5 자의 반환 **문자열** ANSI SQL 표준을 준수 하는 오류 코드를 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **SQLState** SQL 문 처리 하는 동안 오류가 발생 하는 경우 공급자에서 반환 하는 5 자의 오류 코드를 읽을 속성입니다. 예를 들어 Microsoft OLE DB Provider for ODBC와 함께 사용할 경우 Microsoft SQL Server 데이터베이스 SQL 상태 오류 코드에서에서 시작 오류 ODBC에 또는 Microsoft SQL Server에서 발생 하 고 ODBC에 매핑되는 오류를 기반으로 하는 ODBC 오류가 발생 했습니다. 이러한 오류 코드는 ANSI SQL 표준에 설명 되어 있지만 다른 데이터 원본에 의해 다르게 구현 될 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   


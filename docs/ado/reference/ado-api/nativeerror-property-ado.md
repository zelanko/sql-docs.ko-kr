---
title: "NativeError 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords: NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55a6415051943de6b92327ce4e9cf157c972edd4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="nativeerror-property-ado"></a>NativeError 속성 (ADO)
에 대 한 공급자 관련 오류 코드를 나타냅니다는 주어진 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **긴** 오류 코드를 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **NativeError** 특정에 대 한 데이터베이스 관련 오류 정보를 검색할 속성 **오류** 개체입니다. 예를 들어 Microsoft ODBC Provider for OLE DB와 함께 사용할 경우 Microsoft SQL Server 데이터베이스 SQL Server에서 생성 되는 원시 오류 코드 통과 ODBC 및 ODBC 공급자는 ADO **NativeError** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   

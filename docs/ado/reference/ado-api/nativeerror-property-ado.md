---
description: NativeError 속성(ADO)
title: NativeError 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
author: rothja
ms.author: jroth
ms.openlocfilehash: f26e8ab07a5ac51307d3b3da374e982ea5b6f469
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443115"
---
# <a name="nativeerror-property-ado"></a>NativeError 속성(ADO)
지정 된 [오류](../../../ado/reference/ado-api/error-object.md) 개체에 대 한 공급자별 오류 코드를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 오류 코드를 나타내는 **Long** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **NativeError** 속성을 사용 하 여 특정 **오류** 개체에 대 한 데이터베이스 관련 오류 정보를 검색할 수 있습니다. 예를 들어 Microsoft SQL Server 데이터베이스와 OLE DB 용 Microsoft ODBC 공급자를 사용 하는 경우 SQL Server에서 발생 하는 네이티브 오류 코드는 ODBC 및 ODBC 공급자를 통해 ADO **NativeError** 속성에 전달 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   

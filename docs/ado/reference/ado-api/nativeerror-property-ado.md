---
description: NativeError 속성(ADO)
title: NativeError 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 4acc35688367b9508c80c015999aa302a387a55c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990474"
---
# <a name="nativeerror-property-ado"></a>NativeError 속성(ADO)
지정 된 [오류](./error-object.md) 개체에 대 한 공급자별 오류 코드를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 오류 코드를 나타내는 **Long** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **NativeError** 속성을 사용 하 여 특정 **오류** 개체에 대 한 데이터베이스 관련 오류 정보를 검색할 수 있습니다. 예를 들어 Microsoft SQL Server 데이터베이스와 OLE DB 용 Microsoft ODBC 공급자를 사용 하는 경우 SQL Server에서 발생 하는 네이티브 오류 코드는 ODBC 및 ODBC 공급자를 통해 ADO **NativeError** 속성에 전달 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Error 개체](./error-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, Number, Source 및 SQLState 속성 예제 (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)
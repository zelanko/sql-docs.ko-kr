---
title: Field (Visual C++ 구문에 대 한 ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Field collection [ADO], ADO for Visual C++ syntax
ms.assetid: 04631b08-3937-440b-ac09-cd166f239908
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2d5b70e1c00b34c4f1a32822b7896b088d62376
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932779"
---
# <a name="field-ado-for-visual-c-syntax"></a>필드(Visual C++ 구문에 대한 ADO)
## <a name="methods"></a>메서드  
  
```  
AppendChunk(VARIANT Data)  
GetChunk(long Length, VARIANT *pvar)  
```  
  
## <a name="properties"></a>속성  
  
```  
get_ActualSize(long *pl)  
get_Attributes(long *pl)  
put_Attributes(long lAttributes)  
get_DataFormat(IUnknown **ppiDF)  
put_DataFormat(IUnknown *piDF)  
get_DefinedSize(long *pl)  
put_DefinedSize(long lSize)  
get_Name(BSTR *pbstr)  
get_NumericScale(BYTE *pbNumericScale)  
put_NumericScale(BYTE bScale)  
get_OriginalValue(VARIANT *pvar)  
get_Precision(BYTE *pbPrecision)  
put_Precision(BYTE bPrecision)  
get_Type(DataTypeEnum *pDataType)  
put_Type(DataTypeEnum DataType)  
get_UnderlyingValue(VARIANT *pvar)  
get_Value(VARIANT *pvar)  
put_Value(VARIANT Val)  
```  
  
## <a name="see-also"></a>참고 항목  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)

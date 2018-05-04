---
title: 매개 변수 (Visual c + + 구문에 대 한 ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Parameter collection [ADO], ADO for Visual C++ syntax
ms.assetid: 74801dc1-cf0f-4a6e-960b-5990fe55e30d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b666a87f470a8b34a65ded82b332cec14323ad77
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-ado-for-visual-c-syntax"></a>매개 변수 (Visual c + + 구문에 대 한 ADO)
## <a name="methods"></a>메서드  
  
```  
AppendChunk(VARIANT Val)  
```  
  
## <a name="properties"></a>속성  
  
```  
get_Attributes(LONG *plParmAttribs)  
put_Attributes(LONG lParmAttribs)  
get_Direction(ParameterDirectionEnum *plParmDirection)  
put_Direction(ParameterDirectionEnum lParmDirection)  
get_Name(BSTR *pbstr)  
put_Name(BSTR bstr)  
get_NumericScale(BYTE *pbScale)  
put_NumericScale(BYTE bScale)  
get_Precision(BYTE *pbPrecision)  
put_Precision(BYTE bPrecision)  
get_Size(long *pl)  
put_Size(long l)  
get_Type(DataTypeEnum *psDataType)  
put_Type(DataTypeEnum sDataType)  
get_Value(VARIANT *pvar)  
put_Value(VARIANT val)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)

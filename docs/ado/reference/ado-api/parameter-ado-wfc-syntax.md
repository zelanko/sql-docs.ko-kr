---
description: 매개 변수(ADO - WFC 구문)
title: Parameter (ADO-WFC 구문) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fc5226da0ceeefc6ae961b2a3d358d1dc1955b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442825"
---
# <a name="parameter-ado---wfc-syntax"></a>매개 변수(ADO - WFC 구문)
## <a name="package-commswfcdata"></a>package com.  
  
### <a name="constructor"></a>생성자  
  
```  
public Parameter()  
public Parameter(String name)  
public Parameter(String name, int type)  
public Parameter(String name, int type, int dir)  
public Parameter(String name, int type, int dir, int size)  
public Parameter(String name, int type, int dir, int size, Object value)  
```  
  
### <a name="methods"></a>메서드  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
```  
  
### <a name="properties"></a>속성  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getDirection()  
public void setDirection(int dir)  
public String getName()  
public void setName(String name)  
public int getNumericScale()  
public void setNumericScale(int scale)  
public int getPrecision()  
public void setPrecision(int prec)  
public int getSize()  
public void setSize(int size)  
public int getType()  
public void setType(int type)  
public com.ms.com.Variant getValue()  
public void setValue(Object v)  
public AdoProperties getProperties()  
```  
  
## <a name="parameter-accessor-methods"></a>매개 변수 접근자 메서드  
 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체의 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성은 해당 개체의 내용을 가져오거나 설정 합니다. 콘텐츠는 값 및 여러 데이터 형식 중 하나를 할당할 수 있는 개체의 유형인 VARIANT로 표시 됩니다.  
  
 ADO/WFC는 VARIANT 개체를 반환 하는 **getValue** 메서드를 사용 하 여 **Value** 속성을 구현 합니다. 그리고 **setValue** 메서드로 VARIANT를 인수로 사용 합니다. 변형은 Microsoft Visual Basic와 같은 특정 언어에서 매우 효율적입니다.  
  
 ADO/WFC는 **Value** 속성 외에도 Java 데이터 형식을 사용 하 여 **매개 변수** 개체의 내용을 가져오고 설정 하는 *접근자* 메서드를 제공 합니다. 이러한 메서드의 대부분은 **get**_datatype_ 또는 **set**_datatype_형식의 이름을 가집니다.  
  
 한 가지 중요 한 예외가 있습니다. **Getnull** 속성이 없습니다. 대신 필드가 null 인지 여부를 나타내는 부울 값을 반환 하는 **isNull** 속성이 있습니다.  
  
```  
public boolean getBoolean()  
public void setBoolean(boolean v)  
public byte getByte()  
public void setByte(byte v)  
public double getDouble()  
public void setDouble(double v)  
public float getFloat()  
public void setFloat(float v)  
public int getInt()  
public void setInt(int v)  
public long getLong()  
public void setLong(long v)  
public short getShort()  
public void setShort(short v)  
public String getString()  
public void setString(String v)  
public boolean isNull()  
public void setNull()  
```  
  
## <a name="see-also"></a>참고 항목  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)

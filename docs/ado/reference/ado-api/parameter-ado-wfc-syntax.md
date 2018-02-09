---
title: "매개 변수 (ADO-WFC 구문) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 05f3e2f6f6b3985c1c68604e6e9829c1b1f3eef1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="parameter-ado---wfc-syntax"></a>매개 변수 (ADO-WFC 구문)
## <a name="package-commswfcdata"></a>package com.ms.wfc.data  
  
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
 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성은 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 해당 개체의 콘텐츠를 가져오거나 설정 합니다. 콘텐츠 값을 지정할 수 있는 개체의 유형 및 여러 데이터 형식 중 하나는 VARIANT로 표시 됩니다.  
  
 ADO/WFC 구현는 **값** 속성을는 **getValue** 는 VARIANT 개체를 반환 하는 메서드 및 **setValue** 메서드는 VARIANT를 인수로 사용 합니다. Variant는 특정 언어의 경우 Microsoft Visual Basic 등의 매우 효율적입니다.  
  
 이외에 **값** 속성, ADO/WFC 제공 *접근자* Java 데이터 형식 가져오기 및 설정의 내용을 사용 하는 메서드 **매개 변수** 개체입니다. 대부분의 이러한 메서드가 폼의 이름이 **가져오기 * * * DataType* 또는 **설정 * * * DataType*합니다.  
  
 가지 주목할 만한 예외:는 없는 **getNull** 속성 대신는 **isNull** 필드가 null 인지 여부를 나타내는 부울 값을 반환 하는 속성입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)

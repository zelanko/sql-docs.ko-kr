---
title: Field (ADO-WFC 구문) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 583e6de7dc8c3ea05d61dda53c3e630d05e4d5f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918757"
---
# <a name="field-ado---wfc-syntax"></a>필드(ADO - WFC 구문)
## <a name="package-commswfcdata"></a>package com.  
  
### <a name="methods"></a>메서드  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>속성  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 (자세한 내용은 IDataFormat 인터페이스에 대 한 설명서를 참조 하세요.)  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>Field 접근자 메서드  
 [Field](../../../ado/reference/ado-api/field-object.md) 개체의 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성은 해당 개체의 내용을 가져오거나 설정 합니다. 콘텐츠는 값 및 여러 데이터 형식 중 하나를 할당할 수 있는 개체의 유형인 VARIANT로 표시 됩니다.  
  
 ADO/WFC는 VARIANT 개체를 반환 하는 **getValue** 메서드를 사용 하 여 **Value** 속성을 구현 합니다. 그리고 **setValue** 메서드로 VARIANT를 인수로 사용 합니다. 변형은 Microsoft Visual Basic와 같은 특정 언어에서 매우 효율적입니다.  
  
 ADO/WFC는 **Value** 속성 외에도 Java 데이터 형식을 사용 하 여 **Field** 개체의 내용을 가져오고 설정 하는 *접근자* 메서드를 제공 합니다. 이러한 메서드의 대부분은 **get**_datatype_ 또는 **set**_datatype_형식의 이름을 가집니다.  
  
 두 가지 주목할 만한 예외가 있습니다. **getObject** 메서드 중 하나가 지정 된 클래스로 강제 변환 된 개체를 반환 합니다. **Getnull** 속성이 없습니다. 대신 필드가 null 인지 여부를 나타내는 부울 값을 반환 하는 **isNull** 속성이 있습니다.  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>참고 항목  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)

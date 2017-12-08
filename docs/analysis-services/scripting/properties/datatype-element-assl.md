---
title: "DataType 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DataType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DataType
helpviewer_keywords: DataType element
ms.assetid: efe6f717-8288-4ca2-85ed-9b63d27c02d8
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0e0f2ccfcda05eb554dcd20a9c419edb74377bc0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="datatype-element-assl"></a>DataType 요소(ASSL)
  연결된 요소의 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataItem> <!-- or Measure -->  
   ...  
   <DataType>...</DataType>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md), [측정값](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 에 대 한 값 **DataType** 에 정의 된는 **System.Data.OleDb.OleDbType** 열거 합니다. 그러나 다음 표에 열거형 값만에서는 사용할 수는 **DataType** 요소입니다.  
  
|값|Description|  
|-----------|-----------------|  
|*BigInt*|부호 있는 64비트 정수입니다. 이 데이터 형식에 매핑됩니다는 **Int64** 의 데이터 형식이 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB의.NET Framework 및 DBTYPE_I8 데이터 형식입니다.|  
|*Bool*|부울 값입니다. 이 데이터 형식에 매핑됩니다는 **부울** 데이터 형식은.NET Framework 및 OLE DB의 DBTYPE_BOOL 데이터 형식입니다.|  
|*통화*|-2에서 사이의 통화 값<sup>63</sup> (또는-922337203685, 477.5808)에서 2<sup>63</sup>정확도 통화 단위의 1/10, 000 인-1 (또는 + 922,337,203,685,477.5807). 이 데이터 형식에 매핑됩니다는 **10 진수** .NET Framework 및 OLE DB의 DBTYPE_CY 데이터 형식에 대 한 데이터 형식입니다.|  
|*날짜*|배정밀도 부동 소수점 숫자로 저장되는 날짜 데이터입니다. 정수 부분은 1899년 12월 30일 이후의 날짜 수이고, 소수 부분은 하루를 분수로 표시한 수입니다. 이 데이터 형식에 매핑됩니다는 **DateTime** 데이터 형식은.NET Framework 및 OLE DB의 DBTYPE_DATE 데이터 형식입니다.|  
|*Double*|-1.79E+308부터 1.79E+308 사이의 배정밀도 부동 소수점 숫자입니다. 이 데이터 형식에 매핑됩니다는 **Double** .NET Framework 및 OLE DB의 DBTYPE_R8 데이터 형식에 대 한 데이터 형식입니다.|  
|*정수*|부호 있는 32비트 정수입니다. 이 데이터 형식에 매핑됩니다는 **Int32** .NET Framework 및 OLE DB의 DBTYPE_I4 데이터 형식에 대 한 데이터 형식입니다.|  
|*단일*|-3.40E +38부터 3.40E +38 사이의 단정밀도 부동 소수점 숫자입니다. 이 데이터 형식에 매핑됩니다는 **단일** .NET Framework 및 OLE DB의 DBTYPE_R4 데이터 형식에서 데이터 형식입니다.|  
|*SmallInt*|부호 있는 16비트 정수입니다. 이 데이터 형식에 매핑됩니다는 **Int16** .NET Framework 및 OLE DB의 DBTYPE_I2 데이터 형식에 대 한 데이터 형식입니다.|  
|*TinyInt*|부호 있는 8비트 정수입니다. 이 데이터 형식에 매핑됩니다는 **SByte** .NET Framework 및 OLE DB의 DBTYPE_I1 데이터 형식에 대 한 데이터 형식입니다.|  
|*UnsignedBigInt*|부호 없는 64비트 정수입니다. 이 데이터 형식에 매핑됩니다는 **UInt64** 데이터 형식은.NET Framework 및 OLE DB의 DBTYPE_UI8 데이터 형식입니다.|  
|*UnsignedInt*|부호 없는 32비트 정수입니다. 이 데이터 형식에 매핑됩니다는 **UInt32** .NET Framework 및 OLE DB의 DBTYPE_UI4 데이터 형식에 대 한 데이터 형식입니다.|  
|*UnsignedSmallInt*|부호 없는 16비트 정수입니다. 이 데이터 형식에 매핑됩니다는 **UInt16** .NET Framework 및 OLE DB의 DBTYPE_UI2 데이터 형식에 대 한 데이터 형식입니다.|  
|*WChar*|유니코드 문자의 Null로 끝나는 스트림입니다. 이 데이터 형식에 매핑됩니다는 **문자열** 데이터 형식은.NET Framework 및 OLE DB의 DBTYPE_WSTR 데이터 형식입니다.|  
|*상속*|데이터 형식이 고 **DataItem** 에 포함 된는 [소스](../../../analysis-services/scripting/properties/source-element-measure-assl.md) 의 요소는 **측정값** 요소입니다.<br /><br /> 참고:에 적용 **측정값** 요소입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

---
title: 행 집합 및 매개 변수 데이터 형식 매핑 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- DBTYPE_SQLVARIANT data type
- SQL Server Native Client OLE DB provider, data types
- rowsets [OLE DB], data type mapping
- data types [OLE DB]
- GetColumnInfo function
- parameters [OLE DB]
- SSPROP_ALLOWNATIVEVARIANT property
- GetParameterInfo function
- OLE DB, data types
ms.assetid: 3d831ff8-3b79-4698-b2c1-2b5dd2f8235c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b79afdc8917e3a14055b8ada17cbd3d57a8c9f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186413"
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>행 집합 및 매개 변수의 데이터 형식 매핑
  매개 변수 값으로 행 집합에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 나타내는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 OLE DB를 사용 하 여 데이터 정의 데이터 형식, 함수에서 보고 **icolumnsinfo:: Getcolumninfo** 및 **Icommandwithparameters:: Getparameterinfo**합니다.  
  
|SQL Server 데이터 형식|OLE DB 데이터 형식|  
|--------------------------|----------------------|  
|**bigint**|DBTYPE_I8|  
|**binary**|DBTYPE_BYTES|  
|**bit**|DBTYPE_BOOL|  
|**char**|DBTYPE_STR|  
|**datetime**|DBTYPE_DBTIMESTAMP|  
|**datetime2**|DBTYPE_DBTIME2|  
|**decimal**|DBTYPE_NUMERIC|  
|**float**|DBTYPE_R8|  
|**image**|DBTYPE_BYTES|  
|**int**|DBTYPE_I4|  
|**money**|DBTYPE_CY|  
|**nchar**|DBTYPE_WSTR|  
|**ntext**|DBTYPE_WSTR|  
|**numeric**|DBTYPE_NUMERIC|  
|**nvarchar**|DBTYPE_WSTR|  
|**real**|DBTYPE_R4|  
|**smalldatetime**|DBTYPE_DBTIMESTAMP|  
|**smallint**|DBTYPE_I2|  
|**smallmoney**|DBTYPE_CY|  
|**sql_variant**|DBTYPE_VARIANT, DBTYPE_SQLVARIANT|  
|**sysname**|DBTYPE_WSTR|  
|**text**|DBTYPE_STR|  
|**timestamp**|DBTYPE_BYTES|  
|**tinyint**|DBTYPE_UI1|  
|**UDT**|DBTYPE_UDT|  
|**uniqueidentifier**|DBTYPE_GUID|  
|**varbinary**|DBTYPE_BYTES|  
|**varchar**|DBTYPE_STR|  
|**XML**|DBTYPE_XML|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 그림과에서 같이 소비자가 요청한 데이터 변환을 지원 합니다.  
  
 **sql_variant** 개체는 text, ntext, image, varchar(max), nvarchar(max), varbinary(max), xml, timestamp 및 Microsoft .NET Framework CLR(공용 언어 런타임) 사용자 정의 형식을 제외한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식의 데이터를 포함할 수 있습니다. 또한 sql_variant 데이터 인스턴스는 sql_variant를 기본 데이터 형식으로 사용할 수 없습니다. 예를 들어 열의 일부 행에는 **smallint** 값이 포함되고, 다른 행에는 **float** 값이 포함되고, 나머지 행에는 **char**/**nchar** 값이 포함될 수 있습니다.  
  
> [!NOTE]  
>  **sql_variant** 데이터 형식은 Microsoft Visual Basic®의 Variant 데이터 형식 및 OLE DB의 DBTYPE_VARIANT, DBTYPE_SQLVARIANT와 유사합니다.  
  
 **sql_variant** 데이터가 DBTYPE_VARIANT로 인출되면 버퍼의 VARIANT 구조에 배치됩니다. 그러나 VARIANT 구조의 하위 유형이 **sql_variant** 데이터 형식으로 정의된 하위 유형에 매핑되지 않을 수도 있습니다. 모든 하위 유형이 일치하려면 **sql_variant** 데이터가 DBTYPE_SQLVARIANT로 인출되어야 합니다.  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT 데이터 형식  
 지원 하기 위해 합니다 **sql_variant** 데이터 형식으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBTYPE_SQLVARIANT 라는 공급자별 데이터 형식을 노출 합니다. **sql_variant** 데이터가 DBTYPE_SQLVARIANT로 인출되면 공급자별 SSVARIANT 구조에 저장됩니다. SSVARIANT 구조에는 **sql_variant** 데이터 형식의 하위 유형과 일치하는 모든 하위 유형이 포함됩니다.  
  
 또한 세션 속성 SSPROP_ALLOWNATIVEVARIANT를 TRUE로 설정해야 합니다.  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>공급자별 속성 SSPROP_ALLOWNATIVEVARIANT  
 데이터를 인출할 때 열 또는 매개 변수에 대해 반환되어야 하는 데이터 형식 종류를 명시적으로 지정할 수 있습니다. **IColumnsInfo**를 사용하여 열 정보를 가져오고 이 정보를 기반으로 바인딩을 수행할 수도 있습니다. 바인딩 목적을 위해 **IColumnsInfo**를 사용하여 열 정보를 가져오는 경우 SSPROP_ALLOWNATIVEVARIANT 세션 속성이 FALSE(기본값)이면 **sql_variant** 열에 대해 DBTYPE_VARIANT가 반환됩니다. SSPROP_ALLOWNATIVEVARIANT 속성이 FALSE이면 DBTYPE_SQLVARIANT가 지원되지 않습니다. SSPROP_ALLOWNATIVEVARIANT 속성을 TRUE로 설정하면 열 유형이 DBTYPE_SQLVARIANT로 반환되고, 이 경우 버퍼에 SSVARIANT 구조가 포함됩니다. **sql_variant** 데이터를 DBTYPE_SQLVARIANT로 인출하는 경우 세션 속성 SSPROP_ALLOWNATIVEVARIANT를 TRUE로 설정해야 합니다.  
  
 SSPROP_ALLOWNATIVEVARIANT 속성은 공급자별 DBPROPSET_SQLSERVERSESSION 속성 집합의 일부이며 세션 속성입니다.  
  
 DBTYPE_VARIANT는 다른 모든 OLE DB 공급자에 적용됩니다.  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT는 세션 속성이며 DBPROPSET_SQLSERVERSESSION 속성 집합의 일부입니다.  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|형식: VT_BOOL<br /><br /> R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 데이터가 DBTYPE_VARIANT 또는 DBTYPE_SQLVARIANT로 인출되는지를 결정합니다.<br /><br /> VARIANT_TRUE: 열 유형이 DBTYPE_SQLVARIANT로 반환되고, 이 경우 버퍼에 SSVARIANT 구조가 포함됩니다.<br /><br /> VARIANT_FALSE: 열 유형이 DBTYPE_VARIANT로 반환되고, 이 경우 버퍼에 VARIANT 구조가 포함됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 형식 &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  

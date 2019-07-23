---
title: 행 집합 및 매개 변수의 데이터 형식 매핑 | Microsoft Docs
description: 행 집합 및 매개 변수의 데이터 형식 매핑
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- DBTYPE_SQLVARIANT data type
- OLE DB Driver for SQL Server, data types
- rowsets [OLE DB], data type mapping
- data types [OLE DB]
- GetColumnInfo function
- parameters [OLE DB]
- SSPROP_ALLOWNATIVEVARIANT property
- GetParameterInfo function
- OLE DB, data types
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 529c3189676ce704d10a90902bd44f7f2c8e8f6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995209"
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>행 집합 및 매개 변수의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  행 집합과 매개 변수 값으로 SQL Server용 OLE DB 드라이버는 **IColumnsInfo::GetColumnInfo** 및 **ICommandWithParameters::GetParameterInfo** 함수에 보고된 다음 OLE DB 정의 데이터 형식을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 나타냅니다.  
  
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
  
 SQL Server에 대 한 OLE DB 드라이버는 그림에 나와 있는 것 처럼 소비자 요청 데이터 변환을 지원 합니다.  
  
 **sql_variant** 개체는 text, ntext, image, varchar(max), nvarchar(max), varbinary(max), xml, timestamp 및 Microsoft .NET Framework CLR(공용 언어 런타임) 사용자 정의 형식을 제외한 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식의 데이터를 포함할 수 있습니다. 또한 sql_variant 데이터 인스턴스는 sql_variant를 기본 데이터 형식으로 사용할 수 없습니다. 예를 들어 열의 일부 행에는 **smallint** 값이 포함되고, 다른 행에는 **float** 값이 포함되고, 나머지 행에는 **char**/**nchar** 값이 포함될 수 있습니다.  
  
> [!NOTE]  
>  **sql_variant** 데이터 형식은 Microsoft Visual Basic®의 Variant 데이터 형식 및 OLE DB의 DBTYPE_VARIANT, DBTYPE_SQLVARIANT와 유사합니다.  
  
 **sql_variant** 데이터가 DBTYPE_VARIANT로 인출되면 버퍼의 VARIANT 구조에 배치됩니다. 그러나 VARIANT 구조의 하위 유형이 **sql_variant** 데이터 형식으로 정의된 하위 유형에 매핑되지 않을 수도 있습니다. 모든 하위 유형이 일치하려면 **sql_variant** 데이터가 DBTYPE_SQLVARIANT로 인출되어야 합니다.  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT 데이터 형식  
 **sql_variant** 데이터 형식을 지원하기 위해 SQL Server용 OLE DB 드라이버는 DBTYPE_SQLVARIANT라는 공급자별 데이터 형식을 노출합니다. **sql_variant** 데이터가 DBTYPE_SQLVARIANT로 인출되면 공급자별 SSVARIANT 구조에 저장됩니다. SSVARIANT 구조에는 **sql_variant** 데이터 형식의 하위 유형과 일치하는 모든 하위 유형이 포함됩니다.  
  
 또한 세션 속성 SSPROP_ALLOWNATIVEVARIANT를 TRUE로 설정해야 합니다.  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>공급자별 속성 SSPROP_ALLOWNATIVEVARIANT  
 데이터를 인출할 때 열 또는 매개 변수에 대해 반환되어야 하는 데이터 형식 종류를 명시적으로 지정할 수 있습니다. **IColumnsInfo**를 사용하여 열 정보를 가져오고 이 정보를 기반으로 바인딩을 수행할 수도 있습니다. 바인딩 목적을 위해 **IColumnsInfo**를 사용하여 열 정보를 가져오는 경우 SSPROP_ALLOWNATIVEVARIANT 세션 속성이 FALSE(기본값)이면 **sql_variant** 열에 대해 DBTYPE_VARIANT가 반환됩니다. SSPROP_ALLOWNATIVEVARIANT 속성이 FALSE이면 DBTYPE_SQLVARIANT가 지원되지 않습니다. SSPROP_ALLOWNATIVEVARIANT 속성을 TRUE로 설정하면 열 유형이 DBTYPE_SQLVARIANT로 반환되고, 이 경우 버퍼에 SSVARIANT 구조가 포함됩니다. **sql_variant** 데이터를 DBTYPE_SQLVARIANT로 인출하는 경우 세션 속성 SSPROP_ALLOWNATIVEVARIANT를 TRUE로 설정해야 합니다.  
  
 SSPROP_ALLOWNATIVEVARIANT 속성은 공급자별 DBPROPSET_SQLSERVERSESSION 속성 집합의 일부이며 세션 속성입니다.  
  
 DBTYPE_VARIANT는 다른 모든 OLE DB 공급자에 적용됩니다.  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT는 세션 속성이며 DBPROPSET_SQLSERVERSESSION 속성 집합의 일부입니다.  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|유형: VT_BOOL<br /><br /> R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 데이터가 DBTYPE_VARIANT 또는 DBTYPE_SQLVARIANT로 인출되는지를 결정합니다.<br /><br /> VARIANT_TRUE: 열 유형이 DBTYPE_SQLVARIANT로 반환되고, 이 경우 버퍼에 SSVARIANT 구조가 포함됩니다.<br /><br /> VARIANT_FALSE: 열 유형이 DBTYPE_VARIANT로 반환되고, 이 경우 버퍼에 VARIANT 구조가 포함됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식 &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  

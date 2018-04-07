---
title: 행 집합 및 매개 변수 데이터 형식 매핑 | Microsoft Docs
description: 행 집합 및 매개 변수 데이터 형식 매핑
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0470053bebdfd79275afeb629ae54a86a9b2f59e
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>행 집합 및 매개 변수의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server를 나타내는 행 집합 및 매개 변수 값으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다음 OLE DB를 사용 하 여 데이터 정의 함수에 보고 되는 데이터 형식을 **icolumnsinfo:: Getcolumninfo** 및  **Icommandwithparameters:: Getparameterinfo**합니다.  
  
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
  
 OLE DB Driver for SQL Server는 그림과 같이 소비자가 요청한 데이터 변환을 지원 합니다.  
  
 **sql_variant** 개체의 데이터를 저장할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] text, ntext, 이미지, varchar (max), nvarchar (max), varbinary (max), xml, timestamp 및 Microsoft.NET Framework 공용 언어 런타임 (CLR)를 제외 하 고 데이터 형식 사용자 정의 형식입니다. 또한 sql_variant 데이터 인스턴스는 sql_variant를 기본 데이터 형식으로 사용할 수 없습니다. 열이 포함 될 수 있습니다 예를 들어 **smallint** 일부 행에 대 한 값 **float** 다른 행에 대 한 값 및 **char**/**nchar**나머지 부분에는 값입니다.  
  
> [!NOTE]  
>  **sql_variant** Microsoft Visual Basic® 및 DBTYPE_VARIANT, DBTYPE_SQLVARIANT OLEDB에 Variant 데이터 형식을 데이터 형식은 비슷합니다.  
  
 때 **sql_variant** 데이터가 DBTYPE_VARIANT로 인출 되, 버퍼의 VARIANT 구조에 저장 됩니다. 하지만 VARIANT 구조의 하위 형식에 정의 된 하위 유형에 매핑되지 않을 수도 있습니다는 **sql_variant** 데이터 형식입니다. **sql_variant** 데이터 해야 일치 하도록 모든 하위 형식에 대 한 순서 대로 다음 DBTYPE_SQLVARIANT로 인출 하는 수입니다.  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT 데이터 형식  
 지원 하기 위해는 **sql_variant** 데이터 형식에서 OLE DB Driver for SQL Server 노출 DBTYPE_SQLVARIANT 라는 공급자별 데이터 형식입니다. 때 **sql_variant** 데이터가 DBTYPE_SQLVARIANT로 인출 되 고 그 공급자별 SSVARIANT 구조에 저장 됩니다. SSVARIANT 구조 모든 하위 유형과 일치 하는 하위 유형이 포함 된 **sql_variant** 데이터 형식입니다.  
  
 또한 세션 속성 SSPROP_ALLOWNATIVEVARIANT를 TRUE로 설정해야 합니다.  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>공급자별 속성 SSPROP_ALLOWNATIVEVARIANT  
 데이터를 인출할 때 열 또는 매개 변수에 대해 반환되어야 하는 데이터 형식 종류를 명시적으로 지정할 수 있습니다. **IColumnsInfo** 를 한 열 정보를 사용 하는으로 바인딩을 수행할 사용할 수도 있습니다. 때 **IColumnsInfo** SSPROP_ALLOWNATIVEVARIANT 세션 속성이 FALSE (기본값) 이면 DBTYPE_VARIANT에 대해 반환 되 면 바인딩 목적에 대 한 열 정보를 가져오는 데는 **sql_variant**열입니다. SSPROP_ALLOWNATIVEVARIANT 속성이 FALSE이면 DBTYPE_SQLVARIANT가 지원되지 않습니다. SSPROP_ALLOWNATIVEVARIANT 속성을 TRUE로 설정하면 열 유형이 DBTYPE_SQLVARIANT로 반환되고, 이 경우 버퍼에 SSVARIANT 구조가 포함됩니다. 인출 **sql_variant** 데이터를 DBTYPE_SQLVARIANT 세션 속성 SSPROP_ALLOWNATIVEVARIANT TRUE로 설정 되어야 합니다.  
  
 SSPROP_ALLOWNATIVEVARIANT 속성은 공급자별 DBPROPSET_SQLSERVERSESSION 속성 집합의 일부이며 세션 속성입니다.  
  
 DBTYPE_VARIANT는 다른 모든 OLE DB 공급자에 적용됩니다.  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT는 세션 속성이며 DBPROPSET_SQLSERVERSESSION 속성 집합의 일부입니다.  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|형식: VT_BOOL<br /><br /> R/w: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: DBTYPE_VARIANT 또는 DBTYPE_SQLVARIANT로 인출 데이터 인지 여부를 확인 합니다.<br /><br /> VARIANT_TRUE: 열 유형이 DBTYPE_SQLVARIANT로 반환 되는 경우 버퍼 SSVARIANT 구조가 포함 됩니다.<br /><br /> VARIANT_FALSE: 열 유형이 DBTYPE_VARIANT로 반환 되 고 버퍼에 VARIANT 구조가 포함 됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식 & #40; OLE db& #41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  

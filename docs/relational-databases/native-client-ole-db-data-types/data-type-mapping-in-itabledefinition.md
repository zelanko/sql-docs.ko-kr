---
title: ITableDefinition의 데이터 형식 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
ms.assetid: 13292d1f-c17e-4d11-bf98-3460a10cbb18
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 260b2eab13de427473e92a66f4e97ecdaa077376
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429922"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  사용 하 여 테이블을 만들 때를 **itabledefinition:: Createtable** 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 *pwszTypeName* 전달 되는 DBCOLUMNDESC 배열의 멤버입니다. OLE DB 데이터 형식 매핑을 나타내는 소비자 데이터 형식의 열 이름으로 지정 하는 경우는 *wType* DBCOLUMNDESC 구조의 멤버는 무시 됩니다.  
  
 DBCOLUMNDESC 구조를 사용 하 여 OLE DB 데이터 형식을 사용 하 여 새 열 데이터 형식을 지정 하는 경우 *wType* 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 OLE DB 데이터 형식을 다음과 같이 매핑합니다.  
  
|OLE DB 데이터 형식|SQL Server<br /><br /> 데이터 형식|추가 정보|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**이진**하십시오 **varbinary**를 **이미지** 또는 **varbinary (max)**|합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 검사 합니다 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값 및 버전을 기반으로 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **이미지**.<br /><br /> 경우 값 *ulColumnSize* 의 최대 길이 보다 작으면를 **이진** 데이터 형식의 열인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBCOLUMNDESC 검사  *rgPropertySets* 멤버입니다. DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **이진**합니다. 속성의 값이 VARIANT_FALSE 이면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **varbinary**합니다. 두 경우 모두는 DBCOLUMNDESC *ulColumnSize* 멤버 생성 된 SQL Server 열의 너비를 결정 합니다.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBCOLUMDESC 검사 *bPrecision* 및 *bScale* 멤버 전체 자릿수를 확인 하 고 확장 하는 **숫자** 열입니다.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**하십시오 **varchar**를 **텍스트** 또는 **varchar (max)**|합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 검사 합니다 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값 및 버전을 기반으로 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **텍스트**.<br /><br /> 경우 값 *ulColumnSize* 는 멀티 바이트 문자 데이터 형식 열의 최대 길이 보다 작으면 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBCOLUMNDESC 검사 *rgPropertySets*멤버입니다. DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **char**합니다. 속성의 값이 VARIANT_FALSE 이면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **varchar**합니다. 두 경우 모두는 DBCOLUMNDESC *ulColumnSize* 의 너비를 결정 하는 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만든 열입니다.|  
|DBTYPE_UDT|**UDT**|다음 정보는 **DBCOLUMNDESC** 하 여 구조체 **itabledefinition:: Createtable** UDT 열이 필요한 경우:<br /><br /> *pwSzTypeName* is ignored.<br /><br /> *rgPropertySets* 포함 해야 합니다는 **DBPROPSET_SQLSERVERCOLUMN** 속성이 설정 섹션에서 설명한 것 처럼 **DBPROPSET_SQLSERVERCOLUMN**의 [사용자 형식 ](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**하십시오 **nvarchar**합니다 **ntext** 또는 **nvarchar (max)**|합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 검사 합니다 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값을 기준으로 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **ntext**합니다.<br /><br /> 경우 값 *ulColumnSize* 유니코드 문자 데이터 형식 열에는 최대 길이 보다 작은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBCOLUMNDESC 검사 *rgPropertySets*멤버입니다. DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **nchar**합니다. 속성의 값이 VARIANT_FALSE 이면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 매핑합니다 **nvarchar**합니다. 두 경우 모두는 DBCOLUMNDESC *ulColumnSize* 의 너비를 결정 하는 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 만든 열입니다.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  새 테이블을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 위 표에 지정된 OLE DB 데이터 형식 열거형 값만 매핑합니다. 다른 OLE DB 데이터 형식의 열로 테이블을 만들려고 하면 오류가 생성됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 형식 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  

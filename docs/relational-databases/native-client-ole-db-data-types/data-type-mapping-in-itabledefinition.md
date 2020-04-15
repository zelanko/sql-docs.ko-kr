---
title: ITableDefinition의 데이터 형식 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3e828efa513db1ace272e59379f77d063220290
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297074"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ITableDefinition::CreateTable** 함수를 사용하여 테이블을 만들 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 때 네이티브 클라이언트 OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB 공급자는 전달되는 DBCOLUMNDESC 배열의 *pwszTypeName* 멤버에서 데이터 형식을 지정할 수 있습니다. 소비자가 열의 데이터 형식을 이름으로 지정하면 DBCOLUMNDESC 구조의 *wType* 멤버로 표시되는 OLE DB 데이터 형식 매핑이 무시됩니다.  
  
 DBCOLUMNDESC 구조 *wType* 멤버를 사용하여 OLE DB 데이터 형식을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 새 열 데이터 형식을 지정하는 경우 네이티브 클라이언트 OLE DB 공급자는 다음과 같이 OLE DB 데이터 형식을 매핑합니다.  
  
|OLE DB 데이터 형식|SQL Server<br /><br /> 데이터 형식|추가 정보|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image** 또는 **varbinary(max)**|네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 DBCOLUMNDESC 구조의 *ulColumnSize* 멤버를 검사합니다. 인스턴스의 값 및 버전에 따라 네이티브 클라이언트 OLE DB 공급자는 형식을 이미지에 매핑합니다. **image** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> *ulColumnSize* 값이 **이진** 데이터 형식 열의 최대 길이보다 작으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자가 DBCOLUMNDESC *rgPropertySets* 멤버를 검사합니다. DBPROP_COL_FIXEDLENGTH VARIANT_TRUE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 OLE DB 공급자는 형식을 **이진에**매핑합니다. 속성 값이 VARIANT_FALSE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 형식을 **varbinary에**매핑합니다. 두 경우 모두 생성되는 SQL Server 열의 너비는 DBCOLUMNDESC *ulColumnSize* 멤버에 따라 결정됩니다.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**Smallint**||  
|DBTYPE_I4|**Int**||  
|DBTYPE_NUMERIC|**숫자**|네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 DBCOLUMDESC *bPrecision* 및 *bScale* 멤버를 검사하여 **숫자** 열의 정밀도와 배율을 결정합니다.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**플 로트**||  
|DBTYPE_STR|**char**, **varchar**, **text** 또는 **varchar(max)**|네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 DBCOLUMNDESC 구조의 *ulColumnSize* 멤버를 검사합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 값과 버전에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 형식을 **텍스트에**매핑합니다.<br /><br /> *ulColumnSize* 값이 다중 바이트 문자 데이터 형식 열의 최대 길이보다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작으면 네이티브 클라이언트 OLE DB 공급자가 DBCOLUMNDESC *rgPropertySets* 멤버를 검사합니다. DBPROP_COL_FIXEDLENGTH VARIANT_TRUE 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 형식을 **char에**매핑합니다. 속성 값이 VARIANT_FALSE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 형식을 **varchar에**매핑합니다. 두 경우 모두 생성되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열의 너비는 DBCOLUMNDESC *ulColumnSize* 멤버에 따라 결정됩니다.|  
|DBTYPE_UDT|**Udt**|UDT 열이 필요한 경우 **ITableDefinition::CreateTable**에서 **DBCOLUMNDESC** 구조에 사용하는 정보는 다음과 같습니다.<br /><br /> *pwSzTypeName*은 무시됩니다.<br /><br /> *rgPropertySets*는 [사용자 정의 형식 사용](../../relational-databases/native-client/features/using-user-defined-types.md)의 **DBPROPSET_SQLSERVERCOLUMN** 섹션에 설명된 대로 **DBPROPSET_SQLSERVERCOLUMN** 속성 집합을 포함해야 합니다.|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** 또는 **nvarchar(max)**|네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 DBCOLUMNDESC 구조의 *ulColumnSize* 멤버를 검사합니다. 값을 기반으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 **ntext에**형식을 매핑합니다.<br /><br /> *ulColumnSize* 값이 유니코드 문자 데이터 형식 열의 최대 길이보다 작으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자가 DBCOLUMNDESC *rgPropertySets* 멤버를 검사합니다. DBPROP_COL_FIXEDLENGTH VARIANT_TRUE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 **nchar에**형식을 매핑합니다. 속성 값이 VARIANT_FALSE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 **nvarchar**에 형식을 매핑합니다. 두 경우 모두 생성되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열의 너비는 DBCOLUMNDESC *ulColumnSize* 멤버에 따라 결정됩니다.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  새 테이블을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 위 표에 지정된 OLE DB 데이터 형식 열거형 값만 매핑합니다. 다른 OLE DB 데이터 형식의 열로 테이블을 만들려고 하면 오류가 생성됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  

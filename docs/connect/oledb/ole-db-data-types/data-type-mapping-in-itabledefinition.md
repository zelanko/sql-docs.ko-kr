---
title: ITableDefinition의 데이터 형식 매핑 | Microsoft Docs
description: ITableDefinition의 데이터 형식 매핑
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 6e209ec9c5000e0cec0be47335561d020f1dcbe3
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43022729"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ITableDefinition::CreateTable** 함수를 사용하여 테이블을 만들 때 SQL Server용 OLE DB 드라이버 소비자는 전달되는 DBCOLUMNDESC 배열의 *pwszTypeName* 멤버에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 지정할 수 있습니다. 소비자가 열의 데이터 형식을 이름으로 지정하면 DBCOLUMNDESC 구조의 *wType* 멤버로 표시되는 OLE DB 데이터 형식 매핑이 무시됩니다.  
  
 새 열 데이터 형식을 DBCOLUMNDESC 구조 *wType* 멤버를 사용하는 OLE DB 데이터 형식으로 지정하면 SQL Server용 OLE DB 드라이버는 OLE DB 데이터 형식을 다음과 같이 매핑합니다.  
  
|OLE DB 데이터 형식|SQL Server<br /><br /> 데이터 형식|추가 정보|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image** 또는 **varbinary(max)**|OLE DB Driver for SQL Server를 검사 합니다 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값 및 버전을 기반으로 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스, OLE DB 드라이버의 SQL Server에 형식을 매핑합니다 **이미지**.<br /><br /> *ulColumnSize* 값이 **binary** 데이터 형식 열의 최대 길이보다 작으면 SQL Server용 OLE DB 드라이버는 DBCOLUMNDESC *rgPropertySets* 멤버를 검사합니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 **이진**합니다. 속성의 값이 VARIANT_FALSE 이면는 OLE DB Driver for SQL Server 형식을 매핑합니다 **varbinary**합니다. 두 경우 모두 생성되는 SQL Server 열의 너비는 DBCOLUMNDESC *ulColumnSize* 멤버에 따라 결정됩니다.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|SQL Server용 OLE DB 드라이버는 DBCOLUMDESC *bPrecision* 및 *bScale* 멤버를 검사하여 **numeric** 열의 전체 자릿수 및 소수 자릿수를 확인합니다.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** 또는 **varchar(max)**|OLE DB Driver for SQL Server를 검사 합니다 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값 및 버전을 기반으로 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스, OLE DB 드라이버의 SQL Server에 형식을 매핑합니다 **텍스트**.<br /><br /> *ulColumnSize* 값이 멀티바이트 문자 데이터 형식 열의 최대 길이보다 작으면 SQL Server용 OLE DB 드라이버는 DBCOLUMNDESC *rgPropertySets* 멤버를 검사합니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 **char**합니다. 속성의 값이 VARIANT_FALSE 이면는 OLE DB Driver for SQL Server 형식을 매핑합니다 **varchar**합니다. 두 경우 모두 생성되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열의 너비는 DBCOLUMNDESC *ulColumnSize* 멤버에 따라 결정됩니다.|  
|DBTYPE_UDT|**UDT**|UDT 열이 필요한 경우 **ITableDefinition::CreateTable**에서 **DBCOLUMNDESC** 구조에 사용하는 정보는 다음과 같습니다.<br /><br /> *pwSzTypeName* 무시 됩니다.<br /><br /> *rgPropertySets* 포함 해야 합니다는 **DBPROPSET_SQLSERVERCOLUMN** 속성이 설정 섹션에서 설명한 것 처럼 **DBPROPSET_SQLSERVERCOLUMN**의 [사용자 형식 ](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** 또는 **nvarchar(max)**|OLE DB Driver for SQL Server를 검사 합니다 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값에 따라는 OLE DB Driver for SQL Server에 형식을 매핑합니다 **ntext**합니다.<br /><br /> *ulColumnSize* 값이 유니코드 문자 데이터 형식 열의 최대 길이보다 작으면 SQL Server용 OLE DB 드라이버는 DBCOLUMNDESC *rgPropertySets* 멤버를 검사합니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 **nchar**합니다. 속성의 값이 VARIANT_FALSE 이면는 OLE DB Driver for SQL Server 형식을 매핑합니다 **nvarchar**합니다. 두 경우 모두 생성되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열의 너비는 DBCOLUMNDESC *ulColumnSize* 멤버에 따라 결정됩니다.|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  새 테이블을 만들 때 SQL Server용 OLE DB 드라이버는 위 표에 지정된 OLE DB 데이터 형식 열거형 값만 매핑합니다. 다른 OLE DB 데이터 형식의 열로 테이블을 만들려고 하면 오류가 생성됩니다.  

## <a name="see-also"></a>참고 항목  
 [데이터 형식 &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  

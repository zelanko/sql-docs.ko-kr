---
title: ITableDefinition의 데이터 형식 매핑 | Microsoft Docs
description: ITableDefinition의 데이터 형식 매핑
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 5758e232b8690055120924c54585915da4c6ac93
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  사용 하 여 테이블을 만들 때는 **itabledefinition:: Createtable** 함수에는 OLE DB Driver for SQL Server 소비자를 지정할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에 *pwszTypeName* 의 멤버는 전달 되는 DBCOLUMNDESC 배열입니다. OLE DB 데이터 형식 매핑, 나타내는 소비자 데이터 형식의 열 이름으로 지정 하는 경우는 *wType* DBCOLUMNDESC 구조의 멤버는 무시 됩니다.  
  
 새 열 데이터 형식을 DBCOLUMNDESC 구조를 사용 하 여 OLE DB 데이터 형식으로 지정 하는 경우 *wType* 멤버에는 OLE DB Driver for SQL Server는 OLE DB 데이터 형식을 다음과 같이 매핑합니다.  
  
|OLE DB 데이터 형식|SQL Server<br /><br /> 데이터 형식|추가 정보|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**이진**, **varbinary**, **이미지** 또는 **varbinary (max)**|검사 하는 OLE DB Driver for SQL Server는 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값 및 버전에 따라는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가, OLE DB Driver SQL Server 형식에 매핑하는 **이미지**합니다.<br /><br /> 하는 경우의 값 *ulColumnSize* 의 최대 길이 보다 작으면는 **이진** 는 OLE DB Driver for SQL Server는 DBCOLUMNDESC 검사 한 다음 데이터 형식 열을 *rgPropertySets*멤버입니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 **이진**합니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 속성의 값이 VARIANT_FALSE 이면 **varbinary**합니다. 두 경우 모두는 DBCOLUMNDESC *ulColumnSize* 멤버 만든 SQL Server 열의 너비를 결정 합니다.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|OLE DB Driver for SQL Server는 DBCOLUMDESC 검사 *bPrecision* 및 *bScale* 전체 자릿수를 결정 하 고 확장에 대 한 멤버는 **숫자** 열입니다.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **텍스트,** 또는 **varchar (max)**|검사 하는 OLE DB Driver for SQL Server는 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값 및 버전에 따라는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가, OLE DB Driver SQL Server 형식에 매핑하는 **텍스트**합니다.<br /><br /> 하는 경우의 값 *ulColumnSize* 가 SQL Server는 DBCOLUMNDESC 검사에 대 한 멀티 바이트 문자 데이터 형식 열을 다음 OLE DB 드라이버의 최대 길이 보다 작은 *rgPropertySets* 멤버입니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 **char**합니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 속성의 값이 VARIANT_FALSE 이면 **varchar**합니다. 두 경우 모두는 DBCOLUMNDESC *ulColumnSize* 의 너비를 결정 하는 멤버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 만든 열입니다.|  
|DBTYPE_UDT|**UDT**|다음 정보를 사용 하는 **DBCOLUMNDESC** 하 여 구조 **itabledefinition:: Createtable** UDT 열이 필요한 경우:<br /><br /> *pwSzTypeName* is ignored.<br /><br /> *rgPropertySets* 포함 되어야 합니다는 **DBPROPSET_SQLSERVERCOLUMN** 속성 설정에 섹션에 설명 된 대로 **DBPROPSET_SQLSERVERCOLUMN**에 [사용자 유형 ](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** 또는 **nvarchar (max)**|검사 하는 OLE DB Driver for SQL Server는 *ulColumnSize* DBCOLUMNDESC 구조의 멤버입니다. 값에 따라는 OLE DB Driver for SQL Server에 형식을 매핑합니다 **ntext**합니다.<br /><br /> 하는 경우의 값 *ulColumnSize* 보다 작습니다. 유니코드 문자 데이터 형식 열에 다음 OLE DB 드라이버의 최대 길이 DBCOLUMNDESC를 검사 하는 SQL Server에 대 한 *rgPropertySets* 멤버입니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 DBPROP_COL_FIXEDLENGTH가 VARIANT_TRUE 이면 **nchar**합니다. OLE DB Driver for SQL Server에 형식을 매핑합니다 속성의 값이 VARIANT_FALSE 이면 **nvarchar**합니다. 두 경우 모두는 DBCOLUMNDESC *ulColumnSize* 의 너비를 결정 하는 멤버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 만든 열입니다.|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  새 테이블을 만들 때만 OLE DB 데이터 형식 열거형 값을 위의 테이블에 지정 된 된 OLE DB Driver for SQL Server에 매핑합니다. 다른 OLE DB 데이터 형식의 열로 테이블을 만들려고 하면 오류가 생성됩니다.  

## <a name="see-also"></a>참고 항목  
 [데이터 형식 & #40; OLE db& #41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  

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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bdf3a1e716fd1de5354b735e353916bab863059c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73774310"
---
# <a name="data-type-mapping-in-itabledefinition"></a>ITableDefinition의 데이터 형식 매핑
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **Itabledefinition:: CreateTable** 함수를 사용 하 여 테이블을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 전달 되는 DBCOLUMNDESC 배열의 *pwszTypeName* 멤버에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 지정할 수 있습니다. 소비자가 열의 데이터 형식을 이름으로 지정하면 DBCOLUMNDESC 구조의 *wType* 멤버로 표시되는 OLE DB 데이터 형식 매핑이 무시됩니다.  
  
 DBCOLUMNDESC structure *Wtype* 멤버를 사용 하 여 OLE DB 데이터 형식을 사용 하 여 새 열 데이터 형식을 지정 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 OLE DB 데이터 형식을 다음과 같이 매핑합니다.  
  
|OLE DB 데이터 형식|SQL Server<br /><br /> 데이터 형식|추가 정보|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image** 또는 **varbinary(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBCOLUMNDESC 구조의 *Ulcolumnsize* 멤버를 검사 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 값 및 버전에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 **image**에 매핑합니다.<br /><br /> *Ulcolumnsize* 값이 **이진** 데이터 형식 열의 최대 길이 보다 작으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT OLE DB 공급자가 DBCOLUMNDESC *rgPropertySets* 멤버를 검사 합니다. DBPROP_COL_FIXEDLENGTH VARIANT_TRUE 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 **이진**에 매핑합니다. 속성의 값이 VARIANT_FALSE 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 **varbinary**에 매핑합니다. 두 경우 모두 생성되는 SQL Server 열의 너비는 DBCOLUMNDESC *ulColumnSize* 멤버에 따라 결정됩니다.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBCOLUMDESC *Bprecision* 및 *bprecision* 멤버를 검사 하 여 **숫자** 열의 전체 자릿수와 소수 자릿수를 확인 합니다.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** 또는 **varchar(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBCOLUMNDESC 구조의 *Ulcolumnsize* 멤버를 검사 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 값 및 버전에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 **텍스트**에 매핑합니다.<br /><br /> *Ulcolumnsize* 값이 멀티 바이트 문자 데이터 형식 열의 최대 길이 보다 작으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 DBCOLUMNDESC *rgPropertySets* 멤버를 검사 합니다. DBPROP_COL_FIXEDLENGTH VARIANT_TRUE 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 **char**에 매핑합니다. 속성의 값이 VARIANT_FALSE 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 **varchar**에 매핑합니다. 두 경우 모두 생성되는 *열의 너비는 DBCOLUMNDESC*ulColumnSize[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 멤버에 따라 결정됩니다.|  
|DBTYPE_UDT|**UDT**|UDT 열이 필요한 경우 **ITableDefinition::CreateTable**에서 **DBCOLUMNDESC** 구조에 사용하는 정보는 다음과 같습니다.<br /><br /> *pwSzTypeName* 은 무시 됩니다.<br /><br /> *rgPropertySets* 은 [사용자 정의 형식 사용](../../relational-databases/native-client/features/using-user-defined-types.md)의 **DBPROPSET_SQLSERVERCOLUMN**에 대 한 섹션에 설명 된 대로 **DBPROPSET_SQLSERVERCOLUMN** 속성 집합을 포함 해야 합니다.|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** 또는 **nvarchar(max)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBCOLUMNDESC 구조의 *Ulcolumnsize* 멤버를 검사 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 값을 기반으로 형식을 **ntext**에 매핑합니다.<br /><br /> *Ulcolumnsize* 값이 유니코드 문자 데이터 형식 열의 최대 길이 보다 작으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 DBCOLUMNDESC *rgPropertySets* 멤버를 검사 합니다. DBPROP_COL_FIXEDLENGTH VARIANT_TRUE 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 **nchar**에 매핑합니다. 속성의 값이 VARIANT_FALSE 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 형식을 **nvarchar**에 매핑합니다. 두 경우 모두 생성되는 *열의 너비는 DBCOLUMNDESC*ulColumnSize[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 멤버에 따라 결정됩니다.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  새 테이블을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 위 표에 지정된 OLE DB 데이터 형식 열거형 값만 매핑합니다. 다른 OLE DB 데이터 형식의 열로 테이블을 만들려고 하면 오류가 생성됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  

---
title: "OLE DB 테이블 반환 매개 변수 형식 지원 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ced157eb9748955b55677c44ecf72c568ea4755
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB 테이블 반환 매개 변수 형식 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  이 항목에서는 테이블 반환 매개 변수에 대한 OLE DB 형식 지원에 대해 설명합니다.  
  
## <a name="table-valued-parameter-rowset-object"></a>테이블 반환 매개 변수 행 집합 개체  
 테이블 반환 매개 변수에 대한 특수한 행 집합 개체를 만들 수 있습니다. ITableDefinitionWithConstraints::CreateTableWithConstraints 또는 iopenrowset:: Openrowset을 사용 하 여 테이블 반환 매개 변수 행 집합 개체를 만듭니다. 이 작업을 수행 하려면 설정는 *eKind* 의 멤버는 *pTableID* 매개 변수를 DBKIND_GUID_NAME로 고 clsid_rowset_inmemory는 *guid* 멤버입니다. 테이블 반환 매개 변수의 서버 유형 이름은에 지정 해야 합니다는 *pwszName* 소속 *pTableID* iopenrowset:: Openrowset을 사용 하는 경우. 테이블 반환 매개 변수 행 집합 개체는 일반 SQL Server Native Client OLE DB 공급자 개체처럼 작동합니다.  
  
```  
const GUID CLSID_ROWSET_TVP =   
{0xc7ef28d5, 0x7bee, 0x443f, {0x86, 0xda, 0xe3, 0x98, 0x4f, 0xcd, 0x4d, 0xf9}};  
  
CoType RowsetTVP  
{  
[mandatory] interface IAccessor;  
[mandatory] interface IColumnsInfo;  
[mandatory] interface IConvertType;  
[mandatory] interface IRowset;  
[mandatory] interface IRowsetInfo;  
[optional]  interface IColumnsRowset;  
[optional]  interface IRowsetChange;  
[optional]  interface ISupportErrorInfo;  
};  
```  
  
## <a name="dbtypetable"></a>DBTYPE_TABLE  
 새 형식 DBTYPE_TABLE은 테이블 형식을 나타냅니다. 이 형식은 DBTYPE이 필요한 여러 OLE DB 인터페이스에서 테이블 반환 매개 변수를 지정합니다.  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE은 DBTYPE_IUNKNOWN과 형식이 동일하며 데이터 버퍼의 개체에 대한 포인터입니다. 바인딩에서 전체 사양에 대 한 소비자는 DBOBJECT 버퍼으로 채웁니다 *iid* 행 집합 개체 인터페이스 (IID_IRowset) 중 하나로 설정 합니다. DBOBJECT를 지정 하지는 바인딩에, IID_IRowset 간주 됩니다.  
  
 DBTYPE_TABLE과 다른 형식 간의 변환은 지원되지 않습니다. IConvertType::CanConvert는 DBTYPE_TABLE로의 변환이 DBTYPE_TABLE 이외의 모든 요청에 대 한 지원 되지 않는 변환에 대 한 S_FALSE를 반환 합니다. 이의 dbconvertflags_parameter 명령 개체입니다.  
  
## <a name="methods"></a>메서드  
 테이블 반환 매개 변수를 지 원하는 OLE DB 방법에 대 한 정보를 참조 하십시오. [OLE DB Table-Valued 매개 변수 형식 지원 &#40; 방법 &#41; ](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>속성  
 테이블 반환 매개 변수를 지 원하는 OLE DB 속성에 대 한 방법에 대 한 자세한 내용은 참조 하십시오. [OLE DB Table-Valued 매개 변수 형식 지원 &#40; 속성 &#41; ](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 반환 매개 변수 사용 &#40; OLE db&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수 사용 &#40; OLE db&#41;를 사용 하 여](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

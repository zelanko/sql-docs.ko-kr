---
title: OLE DB 테이블 반환 매개 변수 형식 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 27ae90e05784c18d85f84daa9955818d3133ad07
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49085269"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB 테이블 반환 매개 변수 형식 지원
  이 항목에서는 테이블 반환 매개 변수에 대한 OLE DB 형식 지원에 대해 설명합니다.  
  
## <a name="table-valued-parameter-rowset-object"></a>테이블 반환 매개 변수 행 집합 개체  
 테이블 반환 매개 변수에 대한 특수한 행 집합 개체를 만들 수 있습니다. ITableDefinitionWithConstraints::CreateTableWithConstraints 또는 iopenrowset:: Openrowset을 사용 하 여 테이블 반환 매개 변수 행 집합 개체를 만듭니다. 이렇게 하려면 *pTableID* 매개 변수의 *eKind* 멤버를 DBKIND_GUID_NAME으로 설정하고 CLSID_ROWSET_INMEMORY를 *guid* 멤버로 지정합니다. 테이블 반환 매개 변수의 서버 유형 이름을 지정 해야 합니다는 *pwszName* 소속 *pTableID* iopenrowset:: Openrowset을 사용 하는 경우. 테이블 반환 매개 변수 행 집합 개체는 일반 SQL Server Native Client OLE DB 공급자 개체처럼 작동합니다.  
  
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
  
 DBTYPE_TABLE은 DBTYPE_IUNKNOWN과 형식이 동일하며 데이터 버퍼의 개체에 대한 포인터입니다. 전체 바인딩 지정을 위해 소비자는 DBOBJECT 버퍼를 채우고 *iid*를 행 집합 개체 인터페이스 중 하나(IID_IRowset)로 설정합니다. 바인딩에 DBOBJECT를 지정하지 않으면 IID_IRowset으로 간주됩니다.  
  
 DBTYPE_TABLE과 다른 형식 간의 변환은 지원되지 않습니다. DBTYPE_TABLE에서 DBTYPE_TABLE로의 변환이 아닌 지원되지 않는 변환을 요청하면 IConvertType::CanConvert에서 S_FALSE를 반환합니다. 이는 명령 개체의 DBCONVERTFLAGS_PARAMETER로 간주됩니다.  
  
## <a name="methods"></a>메서드  
 테이블 반환 매개 변수를 지 원하는 OLE DB 메서드에 대 한 자세한 내용은 [OLE DB Table-Valued 매개 변수 형식 지원 &#40;메서드&#41;](ole-db-table-valued-parameter-type-support-methods.md)합니다.  
  
## <a name="properties"></a>속성  
 테이블 반환 매개 변수를 지 원하는 OLE DB 속성에 대 한 정보를 참조 하세요 [OLE DB Table-Valued 매개 변수 형식 지원 &#40;속성&#41;](ole-db-table-valued-parameter-type-support-properties.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수&#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

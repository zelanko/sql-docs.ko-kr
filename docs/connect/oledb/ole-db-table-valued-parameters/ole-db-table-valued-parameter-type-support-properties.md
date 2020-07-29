---
title: OLE DB 테이블 반환 매개 변수 형식 지원(속성) | Microsoft Docs
description: OLE DB 테이블 반환 매개 변수 형식 지원(속성)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (properties)
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 476c45419d57d71f48028dc6b103e41e2d8dfa9b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008732"
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>OLE DB 테이블 반환 매개 변수 형식 지원(속성)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 항목에서는 테이블 반환 매개 변수 행 집합 개체와 연관된 OLE DB 속성 및 속성 집합에 대한 정보를 제공합니다.  
  
## <a name="properties"></a>속성  
 다음은 테이블 반환 매개 변수 행 집합 개체에 대한 IRowsetInfo::GetProperties 메서드를 통해 표시되는 속성 목록입니다. 모든 테이블 반환 매개 변수 행 집합 속성은 읽기 전용입니다. 따라서 IOpenRowset::OpenRowset 또는 ITableDefinitionWithConstraints::CreateTableWithConstraints 메서드를 통해 기본값이 아닌 값을 속성으로 설정하려고 하면 오류가 발생하고 개체가 생성되지 않습니다.  
  
 테이블 반환 매개 변수 행 집합 개체에 구현되지 않은 속성은 다음 목록에 없습니다. 전체 속성 목록을 보려면 Windows Data Access Components의 OLE DB 설명서를 참조하십시오.  
  
|속성 ID|값|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|R/W: 읽기 전용<br /><br /> Default: VARIANT_FALSE<br /><br /> 설명: 테이블 반환 매개 변수 행 집합 개체에 책갈피가 허용되지 않습니다.|  
|DBPROP_BOOKMARKSKIPPED|VARIANT_FALSE|  
|DBPROP_BOOKMARKTYPE|DBPROPVAL_BMK_NUMERIC|  
|DBPROP_CANHOLDROWS|VARIANT_FALSE|  
|DBPROP_CHANGEINSERTEDROWS|VARIANT_TRUE|  
|DBPROP_COLUMNRESTRICT|VARIANT_FALSE|  
|DBPROP_COMMANDTIMEOUT|0|  
|DBPROP_COMMITPRESERVE|VARIANT_TRUE|  
|DBPROP_DEFERRED|VARIANT_FALSE|  
|DBPROP_DELAYSTORAGEOBJECTS|VARIANT_FALSE|  
|DBPROP_IAccessor<br /><br /> DBPROP_IColumnsInfo<br /><br /> DBPROP_IConvertType<br /><br /> DBPROP_IRowset<br /><br /> DBPROP_IRowsetInfo<br /><br /> DBPROP_IColumnsRowset|VARIANT_TRUE|  
|DBPROP_IConnectionPointContainer<br /><br /> DBPROP_IMultipleResults<br /><br /> DBPROP_IRowsetUpdate<br /><br /> DBPROP_IRowsetIdentity<br /><br /> DBPROP_IRowsetLocate<br /><br /> DBPROP_IRowsetScroll<br /><br /> DBPROP_IRowsetResynch|VARIANT_FALSE|  
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> 참고: 테이블 반환 매개 변수 행 집합 개체는 IRowsetChange 인터페이스를 지원합니다.<br /><br /> DBPROP_IRowsetChange = VARIANT_TRUE를 사용하여 만들어진 행 집합은 즉시 업데이트 모드 동작을 나타냅니다.<br /><br /> 그러나 BLOB 열이 ISequentialStream 개체로 바인딩된 경우 소비자는 테이블 반환 매개 변수 행 집합 개체가 사용되는 동안 열을 유지해야 합니다.|  
|DBPROP_ISupportErrorInfo|VARIANT_TRUE|  
|DBPROP_ISequentialStream|VARIANT_TRUE|  
|DBPROP_IMMOBILEROWS|VARIANT_TRUE|  
|DBPROP_LITERALIDENTITY|VARIANT_TRUE|  
|DBPROP_LOCKMODE|DBPROPVAL_LM_NONE|  
|DBPROP_MAXOPENROWS|0|  
|DBPROP_MAXPENDINGROWS|0|  
|DBPROP_MAXROWS|0|  
|DBPROP_NOTIFICATIONPHASES|0|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|0|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE|VARIANT_FALSE|  
|DBPROP_OWNINSERT<br /><br /> DBPROP_OWNUPDATEDELETE|VARIANT_TRUE|  
|DBPROP_QUICKRESTART|VARIANT_TRUE|  
|DBPROP_REENTRANTEVENTS|VARIANT_FALSE|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|  
|DBPROP_RETURNPENDINGINSERTS|VARIANT_TRUE|  
|DBPROP_ROWRESTRICT|VARIANT_FALSE|  
|DBPROP_ROWTHREADMODEL|DBPROPVAL_RT_FREETHREAD|  
|DBPROP_SERVERCURSOR|VARIANT_FALSE|  
|DBPROP_SERVERDATAONINSERT|VARIANT_FALSE|  
|DBPROP_STRONGIDENTITY|VARIANT_TRUE|  
|DBPROP_TRANSACTEDOBJECT|VARIANT_FALSE|  
|DBPROP_UNIQUEROWS|VARIANT_FALSE|  
|DBPROP_UPDATABILITY|DBPROPVAL_UP_CHANGE &#124; DBPROPVAL_UP_DELETE &#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>속성 집합  
 다음 속성 집합은 테이블 반환 매개 변수를 지원합니다.  
  
### <a name="dbpropset_sqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 이 속성은 소비자가 필요한 경우 DBCOLUMNDESC 구조체를 통해 각 열에 대해 ITableDefinitionWithConstraints::CreateTableWithConstraints를 사용하여 테이블 반환 매개 변수 행 집합 개체를 만드는 프로세스에서 사용합니다.  
  
|속성 ID|속성 값|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|R/W: 읽기/쓰기<br /><br /> Default: VARIANT_FALSE<br /><br /> 유형: VT_BOOL<br /><br /> 설명: VARIANT_TRUE로 설정된 경우 열이 계산 열임을 나타냅니다. VARIANT_FALSE는 열이 계산 열이 아님을 나타냅니다.|  
  
### <a name="dbpropset_sqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 이러한 속성은 소비자가 ISSCommandWithParameters::GetParameterProperties에 대한 호출에서 테이블 반환 매개 변수 형식 정보를 검색하는 동안 읽혀지고, 소비자가 ISSCommandWithParameters::SetParameterProperties를 통해 테이블 반환 매개 변수에 대한 특정 속성을 설정하는 동안 설정됩니다.  
  
 다음 표에서는 이러한 속성에 대해 자세히 설명합니다.  
  
|속성 ID|속성 값|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|R/W: 읽기/쓰기<br /><br /> Default: VT_EMPTY<br /><br /> 유형: VT_BSTR<br /><br /> 설명: 소비자는 이 속성을 사용하여 테이블 반환 매개 변수 형식 이름을 가져오거나 설정합니다.<br /><br /> 이 속성은 CLR 사용자 정의 형식에도 사용할 수 있습니다.<br /><br /> 이 속성은 필요한 경우 테이블 반환 매개 변수의 테이블 형식 이름을 제공하기 위해 지정할 수 있습니다(ODBC 호출 구문 명령의 경우). 매개 변수가 있는 임시 SQL 쿼리에는 이 속성을 반드시 지정해야 합니다.|  
|SSPROP_PARAM_TYPE_SCHEMANAME|R/W: 읽기/쓰기<br /><br /> Default: VT_EMPTY<br /><br /> 유형: VT_BSTR<br /><br /> 설명: 소비자는 이 속성을 사용하여 테이블 반환 매개 변수 형식 스키마 이름을 가져오거나 설정합니다.<br /><br /> 이 속성은 CLR 사용자 정의 형식에도 사용할 수 있습니다.|  
|SSPROP_PARAM_TYPE_CATALOGNAME|R/W: 읽기 전용<br /><br /> Default: VT_EMPTY<br /><br /> 유형: VT_BSTR<br /><br /> 설명: 소비자는 이 속성을 사용하여 테이블 반환 매개 변수 형식 카탈로그 이름을 가져오거나 설정합니다.<br /><br /> 이 속성은 CLR 사용자 정의 형식에도 사용할 수 있습니다. 이 속성을 설정하면 오류가 발생합니다. 사용자 정의 테이블 형식은 해당 형식을 사용하는 테이블 반환 매개 변수와 같은 데이터베이스에 있어야 합니다.|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|R/W: 읽기/쓰기<br /><br /> Default: VT_EMPTY<br /><br /> 유형: VT_UI2 &#124; VT_ARRAY<br /><br /> 설명: 소비자는 이 속성을 사용하여 행 집합에서 기본값으로 취급할 열 집합을 지정할 수 있습니다. 이러한 열에 대해서는 값이 전송되지 않습니다. 공급자가 소비자 행 집합 개체에서 데이터를 인출하는 동안 이러한 열에 대해서는 바인딩이 필요하지 않습니다.<br /><br /> 배열의 각 요소는 행 집합 개체에서 열의 순서를 나타내는 서수여야 합니다. 잘못된 서수를 지정하면 명령 실행 시 오류가 발생합니다.|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|R/W: 읽기/쓰기<br /><br /> Default: VT_EMPTY<br /><br /> 유형: VT_UI2 &#124; VT_ARRAY<br /><br /> 설명: 이 속성은 소비자가 열 데이터의 정렬 순서를 나타내는 힌트를 서버에 제공하는 데 사용합니다. 공급자는 소비자가 지정된 사양을 따른다고 가정하고 어떠한 유효성 검사도 수행하지 않습니다. 서버에서는 이 속성을 사용하여 최적화를 수행합니다.<br /><br /> 각 열에 대한 열 순서 정보는 배열에서 한 쌍의 요소로 나타납니다. 이 쌍의 첫 번째 요소는 열 번호이고 두 번째 요소는 오름차순의 경우 1이고 내림차순의 경우 2입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [OLE DB 테이블 반환 매개 변수 형식 지원](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

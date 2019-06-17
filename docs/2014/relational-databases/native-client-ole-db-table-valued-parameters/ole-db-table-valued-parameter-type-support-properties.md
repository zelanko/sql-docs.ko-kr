---
title: OLE DB 테이블 반환 매개 변수 형식 지원(속성) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (properties)
ms.assetid: b9c4e6ed-fe4f-4ef8-9bc8-784d80d44039
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5cdd19895a1cf91e1c5c8608013cb52482f946c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046538"
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>OLE DB 테이블 반환 매개 변수 형식 지원(속성)
  이 항목에서는 테이블 반환 매개 변수 행 집합 개체와 연관된 OLE DB 속성 및 속성 집합에 대한 정보를 제공합니다.  
  
## <a name="properties"></a>속성  
 다음은 테이블 반환 매개 변수 행 집합 개체에 대한 IRowsetInfo::GetProperties 메서드를 통해 표시되는 속성 목록입니다. 모든 테이블 반환 매개 변수 행 집합 속성은 읽기 전용입니다. 따라서 설정 하려고 iopenrowset:: Openrowset 또는 ITableDefinitionWithConstraints::CreateTableWithConstraints를 통해 속성의 기본이 아닌 값으로 메서드는 오류가 발생 하며 개체가 만들어질 수 있습니다.  
  
 테이블 반환 매개 변수 행 집합 개체에 구현되지 않은 속성은 다음 목록에 없습니다. 전체 속성 목록을 보려면 Windows Data Access Components의 OLE DB 설명서를 참조하십시오.  
  
|속성 ID|값|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|R/W: 읽기 전용<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 설명: 테이블 반환 매개 변수 행 집합 개체에 책갈피가 허용 되지 않습니다.|  
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
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> 참고: 테이블 반환 매개 변수 행 집합 개체 IRowsetChange 인터페이스를 지원합니다.<br /><br /> DBPROP_IRowsetChange = VARIANT_TRUE를 사용하여 만들어진 행 집합은 즉시 업데이트 모드 동작을 나타냅니다.<br /><br /> 그러나 BLOB 열이 ISequentialStream 개체로 바인딩된 경우 소비자는 테이블 반환 매개 변수 행 집합 개체가 사용되는 동안 열을 유지해야 합니다.|  
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
|DBPROP_UPDATABILITY|DBPROPVAL_UP_CHANGE &AMP;#124; DBPROPVAL_UP_DELETE &AMP;#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>속성 집합  
 다음 속성 집합은 테이블 반환 매개 변수를 지원합니다.  
  
### <a name="dbpropsetsqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 이 속성은 필요한 경우 DBCOLUMNDESC 구조를 통해 각 열에 대해 ITableDefinitionWithConstraints::CreateTableWithConstraints를 사용 하 여 테이블 반환 매개 변수 행 집합 개체를 만드는 프로세스는 소비자가 사용 됩니다.  
  
|속성 ID|속성 값|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|R/W: 읽기/쓰기<br /><br /> 기본값: VARIANT_FALSE<br /><br /> 형식: VT_BOOL<br /><br /> 설명: Variant_true로 설정 하면 열이 계산된 열 임을 나타냅니다. VARIANT_FALSE는 열이 계산 열이 아님을 나타냅니다.|  
  
### <a name="dbpropsetsqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 이러한 속성은 isscommandwithparameters:: Getparameterproperties에 대 한 호출에서 테이블 반환 매개 변수 형식 정보를 검색 하는 동안 읽히고 소비자 및 테이블 반환 매개 변수에 대 한 특정 속성을 설정 하는 동안 소비자가 설정 isscommandwithparameters:: Setparameterproperties를 통해.  
  
 다음 표에서는 이러한 속성에 대해 자세히 설명합니다.  
  
|속성 ID|속성 값|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|R/W: 읽기/쓰기<br /><br /> 기본값: VT_EMPTY<br /><br /> 형식: VT_BSTR<br /><br /> 설명: 소비자는 테이블 반환 매개 변수 형식의 이름을 가져오거나 설정 하려면이 속성을 사용 합니다.<br /><br /> 이 속성은 CLR 사용자 정의 형식에도 사용할 수 있습니다.<br /><br /> 이 속성은 필요한 경우 테이블 반환 매개 변수의 테이블 형식 이름을 제공하기 위해 지정할 수 있습니다(ODBC 호출 구문 명령의 경우). 매개 변수가 있는 임시 SQL 쿼리에는 이 속성을 반드시 지정해야 합니다.|  
|SSPROP_PARAM_TYPE_SCHEMANAME|R/W: 읽기/쓰기<br /><br /> 기본값: VT_EMPTY<br /><br /> 형식: VT_BSTR<br /><br /> 설명: 소비자는 테이블 반환 매개 변수 형식 스키마 이름을 가져오거나 설정 하려면이 속성을 사용 합니다.<br /><br /> 이 속성은 CLR 사용자 정의 형식에도 사용할 수 있습니다.|  
|SSPROP_PARAM_TYPE_CATALOGNAME|R/W: 읽기 전용<br /><br /> 기본값: VT_EMPTY<br /><br /> 형식: VT_BSTR<br /><br /> 설명: 소비자가이 속성을 사용 하 여 테이블 반환 매개 변수 형식 카탈로그 이름을 가져오거나 설정 합니다.<br /><br /> 이 속성은 CLR 사용자 정의 형식에도 사용할 수 있습니다. 이 속성을 설정하면 오류가 발생합니다. 사용자 정의 테이블 형식은 해당 형식을 사용하는 테이블 반환 매개 변수와 같은 데이터베이스에 있어야 합니다.|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|R/W: 읽기/쓰기<br /><br /> 기본값: VT_EMPTY<br /><br /> 형식: VT_UI2 &#124; VT_ARRAY<br /><br /> 설명: 소비자가이 속성을 사용 지정 행 집합의 열 집합으로 간주 됩니다. 이러한 열에 대해서는 값이 전송되지 않습니다. 공급자가 소비자 행 집합 개체에서 데이터를 인출하는 동안 이러한 열에 대해서는 바인딩이 필요하지 않습니다.<br /><br /> 배열의 각 요소는 행 집합 개체에서 열의 순서를 나타내는 서수여야 합니다. 잘못된 서수를 지정하면 명령 실행 시 오류가 발생합니다.|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|R/W: 읽기/쓰기<br /><br /> 기본값: VT_EMPTY<br /><br /> 형식: VT_UI2 &#124; VT_ARRAY<br /><br /> 설명: 이 속성은 서버 정렬에 대 한 힌트를 제공 하는 소비자가 사용 열 데이터의 순서입니다. 공급자는 소비자가 지정된 사양을 따른다고 가정하고 어떠한 유효성 검사도 수행하지 않습니다. 서버에서는 이 속성을 사용하여 최적화를 수행합니다.<br /><br /> 각 열에 대한 열 순서 정보는 배열에서 한 쌍의 요소로 나타납니다. 이 쌍의 첫 번째 요소는 열 번호이고 두 번째 요소는 오름차순의 경우 1이고 내림차순의 경우 2입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 테이블 반환 매개 변수 형식 지원](ole-db-table-valued-parameter-type-support.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](table-valued-parameters-ole-db.md)  
  
  

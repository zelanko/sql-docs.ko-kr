---
title: OLE DB 테이블 반환 매개 변수 형식 지원 (메서드) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (methods)
ms.assetid: e3c2a450-8fd4-44cb-93d8-affe1b65c68e
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e7a22684fabd74400a280396c696c7936081a8d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184472"
---
# <a name="ole-db-table-valued-parameter-type-support-methods"></a>OLE DB 테이블 반환 매개 변수 형식 지원(메서드)
  다음 표준 OLE DB 메서드는 테이블 반환 매개 변수를 지원합니다.  
  
|메서드|테이블 반환 매개 변수 지원|  
|------------|-------------------------------------|  
|ITableDefinitionWithConstraints::CreateTableWithConstraints|테이블 반환 매개 변수의 형식 정보를 알고 있으며 해당 형식 정보를 기반으로 테이블 반환 매개 변수 행 집합 개체를 인스턴스화하려는 경우 사용합니다.<br /><br /> 자세한 내용은 "정적 시나리오"를 참조 [테이블 반환 매개 변수 행 집합을 만들지](table-valued-parameter-rowset-creation.md)합니다.|  
|IOpenRowset::OpenRowset|테이블 반환 매개 변수의 형식 정보를 알지 못하며 서버에서 검색된 메타데이터 정보를 기반으로 테이블 반환 매개 변수 행 집합 개체를 인스턴스화하려는 경우 사용합니다.<br /><br /> 자세한 내용은 "동적 시나리오"를 참조 [테이블 반환 매개 변수 행 집합을 만들지](table-valued-parameter-rowset-creation.md)합니다.|  
|ISSCommandWithParameters::SetParameterInfo|테이블 반환 매개 변수의 명령 매개 변수를 지정 하려면 소비자에서 형식을 지정 된 매개 변수의 "table" 또는 "DBTYPE_TABLE"로 *pwszName* DBPARAMBINDINFO 구조체의 멤버입니다. *ulParamSize* 로 설정 된 ~ 0입니다. 자세한 내용은의 "테이블 반환 매개 변수 사양" 참조 [Executing Commands Containing Table-Valued 매개 변수](executing-commands-containing-table-valued-parameters.md)합니다.|  
|ISSCommandWithParameters::SetParameterProperties|스키마 이름, 유형 이름, 열 순서, 기본 열과 같은 테이블 반환 매개 변수와 관련된 속성을 설정합니다.<br /><br /> 매개 변수의 서 수를 지정 하는 소비자는 *iOrdinal* SSPARAMPROPS 구조의 합니다. 요청되는 속성 집합은 DBPROPSET_SQLSERVERPARAMETER입니다.|  
|ISSCommandWithParameters::GetParameterInfo|모든 매개 변수 형식을 지정된 명령으로 가져옵니다.<br /><br /> 테이블 반환 매개 변수는 *wType* DBPARAMINFO 구조에는 필드는 DBTYPE_TABLE 형식이 갖습니다. *ulParamSize* 필드로 설정 됩니다 ~를 알 수 없는 길이 나타내는 0입니다.|  
|ISSCommandWithParameters::GetParameterProperties|DBTYPE_TABLE 형식의 매개 변수에 대한 추가적인 형식 정보를 가져옵니다.<br /><br /> 매개 변수의 서 수를 지정 하는 소비자는 *iOrdinal* SSPARAMPROPS 구조체의 멤버입니다. 소비자는 isscommandwithparameters:: Setparameterproperties 아래 나열 되어 있는 DBPROPSET_SQLSERVERPARAMETER 속성 집합의 속성 중 하나를 요청할 수 있습니다.<br /><br /> 소비자가 테이블 반환 매개 변수 형식을 알 수 없기 때문에 공급자가 SSPROP_PARAM_TYPE_TYPENAME, SSPROP_PARAM_TYPE_SCHEMANAME 및 SSPROP_PARAM_TYPE_CATALOGNAME을 올바른 값으로 설정해야 합니다. 나머지 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 및 SSPROP_PARAM_TABLE_COLUMN_SORT_ORDER 속성에는 기본값이 사용됩니다. 소비자가 테이블 반환 매개 변수 형식 이름을 검색 한 후에 iopenrowset:: Openrowset을 사용 하 여의이 테이블 반환 매개 변수를 테이블 반환 매개 변수 형식 이름을 지정 하는 인스턴스를 만듭니다. 자세한 내용은 참조 [테이블 반환 매개 변수 형식 검색](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md)합니다.|  
|IRowsetInfo::GetProperties|테이블 반환 매개 변수 행 집합 속성을 가져옵니다. 소비자는 이 속성을 사용하여 최적의 바인딩을 설정할 수 있습니다.|  
|IColumnsRowset::GetColumnsRowset|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 대한 메타데이터 정보를 검색합니다. 테이블 반환 매개 변수의 경우에는 동일한 인터페이스에서 다음과 같은 각 열에 대한 자세한 메타데이터 정보를 제공합니다.<br /><br /> -DBCOLUMN_FLAGS는 DBCOLUMNFLAGS_ISNULLABLE 비트를 통해 null 허용 여부를 나타냅니다.<br />-DBCOLUMN_ISUNIQUE는 열이 id 열인지 여부를 나타냅니다.<br />-DBCOLUMN_COMPUTEMODE는 열이 계산 되 고 있는지 여부를 나타냅니다.|  
|IAccessor::CreateAccessor|와 접근자를 만들 테이블 반환 매개 변수 행 집합 개체는 명령 매개 변수를 바인딩하려면 해당 *wType* 멤버가 DBTYPE_TABLE로 설정 합니다. DBOBJECT 구조는 IID_IRowset 또는 다른 모든 유효한 행 집합 개체 인터페이스에 포함 됩니다는 *iid* 멤버입니다. 나머지 필드는 DBTYPE_IUNKNOWN과 유사하게 처리됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 테이블 반환 매개 변수 형식 지원](ole-db-table-valued-parameter-type-support.md)   
 [테이블 반환 매개 변수 행 집합 만들기](table-valued-parameter-rowset-creation.md)   
 [테이블 반환 매개 변수를 사용 하 여 &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)  
  
  
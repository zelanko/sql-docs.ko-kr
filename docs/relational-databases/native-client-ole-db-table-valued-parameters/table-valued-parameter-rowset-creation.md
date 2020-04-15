---
title: 테이블 반환 매개 변수 행 집합 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab3541f354af26f32f4071c2a6d09648cd53af6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283193"
---
# <a name="table-valued-parameter-rowset-creation"></a>테이블 반환 매개 변수 행 집합 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  소비자는 테이블 반환 매개 변수에 대해 모든 행 집합 개체를 제공할 수 있지만 일반적으로 행 집합 개체는 백 엔드 데이터 저장소에 대해 구현되므로 성능이 제한되는 경우가 많습니다. 이러한 이유로 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하여 메모리 내 데이터에 대해 특수화된 행 집합 개체를 만들 수 있습니다. 이 특별한 메모리 내 행 집합 개체는 테이블 값 매개 변수 행 집합이라는 새 COM 개체입니다. 이 개체는 매개 변수 집합과 비슷한 기능을 제공합니다.  
  
 테이블 반환 매개 변수 행 집합 개체는 소비자가 여러 세션 수준 인터페이스를 통해 입력 매개 변수에 대해서 명시적으로 생성합니다. 테이블 반환 매개 변수 행 집합 개체의 인스턴스는 테이블 반환 매개 변수당 하나씩 생성됩니다. 소비자는 이미 알려진 메타데이터 정보를 제공(정적 시나리오)하거나 공급자 인터페이스를 통해 해당 정보를 검색(동적 시나리오)하는 방법으로 테이블 반환 매개 변수 행 집합 개체를 만들 수 있습니다. 다음 섹션에서는 이러한 두 시나리오에 대해 설명합니다.  
  
## <a name="static-scenario"></a>정적 시나리오  
 형식 정보가 알려져 있는 경우, 소비자는 ITableDefinitionWithConstraints::CreateTableWithConstraints를 사용하여 테이블 반환 매개 변수에 해당하는 테이블 반환 매개 변수 행 집합 개체를 인스턴스화합니다.  
  
 *guid* 필드(*pTableID* 매개 변수)에는 특별한 GUID(CLSID_ROWSET_TVP)가 포함되어 있습니다. *pwszName* 멤버에는 소비자가 인스턴스화할 테이블 반환 매개 변수 형식의 이름이 포함되어 있습니다. *eKind* 필드는 DBKIND_GUID_NAME으로 설정됩니다. 이 이름은 문이 임시 SQL일 때 필요하며 문이 프로시저 호출일 때는 선택 사항입니다.  
  
 소비자는 집계를 위해 제어용 IUnknown을 사용하여 *pUnkOuter* 매개 변수를 전달합니다.  
  
 테이블 값 매개 변수 행 집합 개체 속성만 읽혀지므로 소비자는 *rgPropertySet에서*속성을 설정하지 않을 것으로 예상됩니다.  
  
 각 DBCOLUMNDESC 구조의 *rgPropertySets* 멤버에 대해 소비자는 각 열의 추가 속성을 지정할 수 있습니다. 이러한 속성은 DBPROPSET_SQLSERVERCOLUMN 속성 집합에 속하며 각 열에 대해 계산된 설정과 기본 설정을 지정할 수 있도록 해 줍니다. 또한 Null 허용 여부나 ID 같은 기존 열 속성도 지원합니다.  
  
 소비자는 테이블 반환 매개 변수 행 집합 개체에서 해당 정보를 검색하기 위해 IRowsetInfo::GetProperties를 사용합니다.  
  
 각 열의 null, 고유, 계산 및 업데이트 상태에 대한 정보를 검색하려면 소비자는 IColumnsRowset::GetColumnsRowset 또는 IColumnsInfo:GetColumnInfo를 사용합니다. 이러한 메서드는 각 테이블 반환 매개 변수 행 집합 열에 대해 자세한 정보를 제공합니다.  
  
 소비자는 테이블 반환 매개 변수의 각 열 유형을 지정합니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이블을 만든 경우 열을 지정하는 방법과 비슷합니다. 소비자는 *ppRowset* 출력 매개 변수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통해 네이티브 클라이언트 OLE DB 공급자로부터 테이블 값 매개 변수 행 집합 개체를 가져옵니다.  
  
## <a name="dynamic-scenario"></a>동적 시나리오  
 소비자에 형식 정보가 없는 경우 IOpenRowset::OpenRowset을 사용하여 테이블 값 매개 변수 행 집합 개체를 인스턴스화해야 합니다. 이때 소비자는 공급자에게 유형 이름을 제공해야 합니다.  
  
 이 시나리오에서는 공급자가 소비자 대신 서버에서 테이블 반환 매개 변수 행 집합 개체에 대한 유형 정보를 가져옵니다.  
  
 *pTableID* 및 *pUnkOuter* 매개 변수는 정적 시나리오의 경우와 마찬가지로 설정해야 합니다. 그런 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 네이티브 클라이언트 OLE DB 공급자는 서버에서 형식 정보(열 정보 및 제약 조건)를 가져오고 *ppRowset* 매개 변수를 통해 테이블 값 매개 변수 행 집합 개체를 반환합니다. 이 경우 서버와의 통신이 필요하므로 이 작업은 정적 시나리오와 같은 방식으로 수행되지 않습니다. 동적 시나리오는 매개 변수가 있는 프로시저 호출의 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [OLE DB &#40;테이블 값 매개 변수&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

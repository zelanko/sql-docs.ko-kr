---
title: 테이블 반환 매개 변수 행 집합 만들기 | Microsoft Docs
description: 정적 및 동적 테이블 반환 매개 변수 행 집합 만들기
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 2b8e85b4ebfa679dda4e980df54cd11a06b1946d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805401"
---
# <a name="table-valued-parameter-rowset-creation"></a>테이블 반환 매개 변수 행 집합 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  소비자는 테이블 반환 매개 변수에 대해 모든 행 집합 개체를 제공할 수 있지만 일반적으로 행 집합 개체는 백 엔드 데이터 저장소에 대해 구현되므로 성능이 제한되는 경우가 많습니다. 이러한 이유로 소비자는 SQL Server용 OLE DB 드라이버를 사용하여 메모리 내 데이터에 대해 특수화된 행 집합 개체를 만들 수 있습니다. 이 특수한 메모리 내 행 집합 개체는 테이블 반환 매개 변수 행 집합이라고 하는 새로운 COM 개체입니다. 이 개체는 매개 변수 집합과 비슷한 기능을 제공합니다.  
  
 테이블 반환 매개 변수 행 집합 개체는 소비자가 여러 세션 수준 인터페이스를 통해 입력 매개 변수에 대해서 명시적으로 생성합니다. 테이블 반환 매개 변수 행 집합 개체의 인스턴스는 테이블 반환 매개 변수당 하나씩 생성됩니다. 소비자는 이미 알려진 메타데이터 정보를 제공(정적 시나리오)하거나 공급자 인터페이스를 통해 해당 정보를 검색(동적 시나리오)하는 방법으로 테이블 반환 매개 변수 행 집합 개체를 만들 수 있습니다. 다음 섹션에서는 이러한 두 시나리오에 대해 설명합니다.  
  
## <a name="static-scenario"></a>정적 시나리오  
 형식 정보를 알 경우 소비자 ITableDefinitionWithConstraints::CreateTableWithConstraints을 사용 하 여 테이블 반환 매개 변수에 해당 하는 테이블 반환 매개 변수 행 집합 개체를 인스턴스화합니다.  
  
 합니다 *guid* 필드 (*pTableID* 매개 변수)는 특별 한 GUID (CLSID_ROWSET_TVP)를 포함 합니다. *pwszName* 멤버에는 소비자가 인스턴스화할 테이블 반환 매개 변수 형식의 이름이 포함되어 있습니다. *eKind* 필드는 DBKIND_GUID_NAME으로 설정됩니다. 이 이름은 명령문이 임시 SQL일 때 필요하며 명령문이 프로시저 호출일 때는 선택 사항입니다.  
  
 집계에 대 한 소비자 전달 합니다 *pUnkOuter* controlling IUnknown 사용 하 여 매개 변수입니다.  
  
 테이블 반환 매개 변수 행 집합 개체 속성은 읽기 전용이므로 소비자는 *rgPropertySets*의 속성을 설정할 수 없습니다.  
  
 각 DBCOLUMNDESC 구조의 *rgPropertySets* 멤버에 대해 소비자는 각 열의 추가 속성을 지정할 수 있습니다. 이러한 속성은 DBPROPSET_SQLSERVERCOLUMN 속성 집합에 속하며 각 열에 대해 계산된 설정과 기본 설정을 지정할 수 있도록 해 줍니다. 또한 Null 허용 여부나 ID 같은 기존 열 속성도 지원합니다.  
  
 소비자는 테이블 반환 매개 변수 행 집합 개체에서 해당 정보를 검색하기 위해 IRowsetInfo::GetProperties를 사용합니다.  
  
 계산 열, null, 고유에 대 한 정보를 검색 하 고 각 열의 상태를 업데이트 하려면 소비자 icolumnsrowset:: Getcolumnsrowset 또는 icolumnsinfo:: Getcolumninfo 사용. 이러한 메서드는 각 테이블 반환 매개 변수 행 집합 열에 대해 자세한 정보를 제공합니다.  
  
 소비자는 테이블 반환 매개 변수의 각 열 유형을 지정합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 테이블을 만드는 경우 열을 지정하는 방법과 비슷합니다. 소비자를 통해 SQL Server에 대 한 OLE DB 드라이버에서 테이블 반환 매개 변수 행 집합 개체를 가져옵니다 합니다 *ppRowset* 매개 변수를 출력 합니다.  
  
## <a name="dynamic-scenario"></a>동적 시나리오  
 소비자는 유형 정보가 없는, 하는 경우 테이블 반환 매개 변수 행 집합 개체를 인스턴스화하 iopenrowset:: Openrowset 사용 해야 합니다. 이때 소비자는 공급자에게 유형 이름을 제공해야 합니다.  
  
 이 시나리오에서는 공급자가 소비자 대신 서버에서 테이블 반환 매개 변수 행 집합 개체에 대한 유형 정보를 가져옵니다.  
  
 합니다 *pTableID* 하 고 *pUnkOuter* 정적 시나리오와 같이 매개 변수를 설정 해야 합니다. 그런 다음, SQL Server용 OLE DB 드라이버는 서버에서 유형 정보(열 정보 및 제약 조건)를 가져오고 *ppRowset* 매개 변수를 통해 테이블 반환 매개 변수 행 집합 개체를 반환합니다. 이 경우 서버와의 통신이 필요하므로 이 작업은 정적 시나리오와 같은 방식으로 수행되지 않습니다. 동적 시나리오는 매개 변수가 있는 프로시저 호출의 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 반환 매개 변수&#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

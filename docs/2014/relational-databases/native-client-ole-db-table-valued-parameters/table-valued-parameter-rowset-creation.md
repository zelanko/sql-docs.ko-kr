---
title: 테이블 반환 매개 변수 행 집합 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de130ef821551383ada1a6df3574404cd3518e88
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046518"
---
# <a name="table-valued-parameter-rowset-creation"></a>테이블 반환 매개 변수 행 집합 만들기
  소비자는 테이블 반환 매개 변수에 대해 모든 행 집합 개체를 제공할 수 있지만 일반적으로 행 집합 개체는 백 엔드 데이터 저장소에 대해 구현되므로 성능이 제한되는 경우가 많습니다. 이러한 이유로 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하여 메모리 내 데이터에 대해 특수화된 행 집합 개체를 만들 수 있습니다. 이 특수 한 메모리 행 집합 개체는 테이블 반환 매개 변수 행 집합을 호출 하는 새로운 COM 개체입니다. 이 개체는 매개 변수 집합과 비슷한 기능을 제공합니다.  
  
 테이블 반환 매개 변수 행 집합 개체는 소비자가 여러 세션 수준 인터페이스를 통해 입력 매개 변수에 대해서 명시적으로 생성합니다. 테이블 반환 매개 변수 행 집합 개체의 인스턴스는 테이블 반환 매개 변수당 하나씩 생성됩니다. 소비자는 이미 알려진 메타데이터 정보를 제공(정적 시나리오)하거나 공급자 인터페이스를 통해 해당 정보를 검색(동적 시나리오)하는 방법으로 테이블 반환 매개 변수 행 집합 개체를 만들 수 있습니다. 다음 섹션에서는 이러한 두 시나리오에 대해 설명합니다.  
  
## <a name="static-scenario"></a>정적 시나리오  
 형식 정보를 알 경우 소비자 ITableDefinitionWithConstraints::CreateTableWithConstraints을 사용 하 여 테이블 반환 매개 변수에 해당 하는 테이블 반환 매개 변수 행 집합 개체를 인스턴스화합니다.  
  
 합니다 *guid* 필드 (*pTableID* 매개 변수)는 특별 한 GUID (CLSID_ROWSET_TVP)를 포함 합니다. *pwszName* 멤버에는 소비자가 인스턴스화할 테이블 반환 매개 변수 형식의 이름이 포함되어 있습니다. *eKind* 필드는 DBKIND_GUID_NAME으로 설정됩니다. 이 이름은 문이 임시 SQL일 때 필요하며 문이 프로시저 호출일 때는 선택 사항입니다.  
  
 집계에 대 한 소비자 전달 합니다 *pUnkOuter* controlling IUnknown 사용 하 여 매개 변수입니다.  
  
 테이블 반환 매개 변수 행 집합 개체 속성은 읽기 전용 이므로 소비자 모든 속성을 설정 하려면 필요 하지 않습니다 *rgPropertySets*합니다.  
  
 각 DBCOLUMNDESC 구조의 *rgPropertySets* 멤버에 대해 소비자는 각 열의 추가 속성을 지정할 수 있습니다. 이러한 속성은 DBPROPSET_SQLSERVERCOLUMN 속성 집합에 속하며 각 열에 대해 계산된 설정과 기본 설정을 지정할 수 있도록 해 줍니다. 또한 Null 허용 여부나 ID 같은 기존 열 속성도 지원합니다.  
  
 소비자는 테이블 반환 매개 변수 행 집합 개체에서 해당 정보를 검색하기 위해 IRowsetInfo::GetProperties를 사용합니다.  
  
 계산 열, null, 고유에 대 한 정보를 검색 하 고 각 열의 상태를 업데이트 하려면 소비자 icolumnsrowset:: Getcolumnsrowset 또는 icolumnsinfo:: Getcolumninfo를 사용 합니다. 이러한 메서드는 각 테이블 반환 매개 변수 행 집합 열에 대해 자세한 정보를 제공합니다.  
  
 소비자는 테이블 반환 매개 변수의 각 열 유형을 지정합니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이블을 만든 경우 열을 지정하는 방법과 비슷합니다. 소비자에서 테이블 반환 매개 변수 행 집합 개체를 가져옵니다 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 통해 합니다 *ppRowset* 출력 매개 변수입니다.  
  
## <a name="dynamic-scenario"></a>동적 시나리오  
 소비자에 형식 정보가 없는 경우 테이블 반환 매개 변수 행 집합 개체를 인스턴스화하 iopenrowset:: Openrowset 사용 해야 합니다. 이때 소비자는 공급자에게 유형 이름을 제공해야 합니다.  
  
 이 시나리오에서는 공급자가 소비자 대신 서버에서 테이블 반환 매개 변수 행 집합 개체에 대한 유형 정보를 가져옵니다.  
  
 합니다 *pTableID* 하 고 *pUnkOuter* 정적 시나리오와 같이 매개 변수를 설정 해야 합니다. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음 서버에서 형식 정보 (열 정보 및 제약 조건)을 가져옵니다 및 통해 테이블 반환 매개 변수 행 집합 개체를 반환 합니다 *ppRowset* 매개 변수입니다. 이 경우 서버와의 통신이 필요하므로 이 작업은 정적 시나리오와 같은 방식으로 수행되지 않습니다. 동적 시나리오는 매개 변수가 있는 프로시저 호출의 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수&#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

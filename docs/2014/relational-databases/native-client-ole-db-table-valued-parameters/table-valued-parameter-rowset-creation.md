---
title: 테이블 반환 매개 변수 행 집합을 만들지 | Microsoft Docs
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
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 76c9ba34a9dde069e574d714a042a7a9cf11a9ff
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182795"
---
# <a name="table-valued-parameter-rowset-creation"></a>테이블 반환 매개 변수 행 집합 만들기
  소비자는 테이블 반환 매개 변수에 대해 모든 행 집합 개체를 제공할 수 있지만 일반적으로 행 집합 개체는 백 엔드 데이터 저장소에 대해 구현되므로 성능이 제한되는 경우가 많습니다. 이러한 이유로 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하여 메모리 내 데이터에 대해 특수화된 행 집합 개체를 만들 수 있습니다. 이 특수 한 메모리에 행 집합 개체는 테이블 반환 매개 변수 행 집합 이라고 하는 새로운 COM 개체입니다. 이 개체는 매개 변수 집합과 비슷한 기능을 제공합니다.  
  
 테이블 반환 매개 변수 행 집합 개체는 소비자가 여러 세션 수준 인터페이스를 통해 입력 매개 변수에 대해서 명시적으로 생성합니다. 테이블 반환 매개 변수 행 집합 개체의 인스턴스는 테이블 반환 매개 변수당 하나씩 생성됩니다. 소비자는 이미 알려진 메타데이터 정보를 제공(정적 시나리오)하거나 공급자 인터페이스를 통해 해당 정보를 검색(동적 시나리오)하는 방법으로 테이블 반환 매개 변수 행 집합 개체를 만들 수 있습니다. 다음 섹션에서는 이러한 두 시나리오에 대해 설명합니다.  
  
## <a name="static-scenario"></a>정적 시나리오  
 유형 정보가 알려져, 소비자는 테이블 반환 매개 변수에 해당 하는 테이블 반환 매개 변수 행 집합 개체를 인스턴스화할 ITableDefinitionWithConstraints::CreateTableWithConstraints를 사용 합니다.  
  
 *guid* 필드 (*pTableID* 매개 변수)는 특별 한 GUID (CLSID_ROWSET_TVP)를 포함 합니다. *pwszName* 멤버는 소비자가 인스턴스화할 테이블 반환 매개 변수 형식의 이름을 포함 합니다. *eKind* 필드는 DBKIND_GUID_NAME로 설정 됩니다. 이 이름은 문이 임시 SQL일 때 필요하며 문이 프로시저 호출일 때는 선택 사항입니다.  
  
 집계의 경우 소비자는 다음과 같이 전달 됩니다.는 *pUnkOuter* controlling IUnknown 매개 변수입니다.  
  
 테이블 반환 매개 변수 행 집합 개체 속성은 읽기 전용 이므로 소비자에서 모든 속성을 설정 하지 않아야 *rgPropertySets*합니다.  
  
 에 대 한는 *rgPropertySets* 멤버 소비자 각 DBCOLUMNDESC 구조의 각 열에 대 한 추가 속성을 지정할 수 있습니다. 이러한 속성은 DBPROPSET_SQLSERVERCOLUMN 속성 집합에 속하며 각 열에 대해 계산된 설정과 기본 설정을 지정할 수 있도록 해 줍니다. 또한 Null 허용 여부나 ID 같은 기존 열 속성도 지원합니다.  
  
 소비자는 테이블 반환 매개 변수 행 집합 개체에서 해당 정보를 검색 하려면 irowsetinfo:: Getproperties를 사용 합니다.  
  
 계산, null, 고유에 대 한 정보를 검색 하 고 각 열의 상태를 업데이트 하려면 소비자 icolumnsrowset:: Getcolumnsrowset 또는 icolumnsinfo:: Getcolumninfo를 사용 합니다. 이러한 메서드는 각 테이블 반환 매개 변수 행 집합 열에 대해 자세한 정보를 제공합니다.  
  
 소비자는 테이블 반환 매개 변수의 각 열 유형을 지정합니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이블을 만든 경우 열을 지정하는 방법과 비슷합니다. 소비자는 테이블 반환 매개 변수 행 집합 개체를 가져옵니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 통해는 *ppRowset* 출력 매개 변수입니다.  
  
## <a name="dynamic-scenario"></a>동적 시나리오  
 소비자에 형식 정보가 없는 경우 테이블 반환 매개 변수 행 집합 개체를 인스턴스화하 iopenrowset:: Openrowset을 사용 해야 합니다. 이때 소비자는 공급자에게 유형 이름을 제공해야 합니다.  
  
 이 시나리오에서는 공급자가 소비자 대신 서버에서 테이블 반환 매개 변수 행 집합 개체에 대한 유형 정보를 가져옵니다.  
  
 *pTableID* 및 *pUnkOuter* 매개 변수는 정적 시나리오와 마찬가지로 설정 해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 다음 형식 정보 (열 정보 및 제약 조건) 서버에서 가져오고를 통해 테이블 반환 매개 변수 행 집합 개체를 반환 하는 *ppRowset* 매개 변수입니다. 이 경우 서버와의 통신이 필요하므로 이 작업은 정적 시나리오와 같은 방식으로 수행되지 않습니다. 동적 시나리오는 매개 변수가 있는 프로시저 호출의 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수 &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수를 사용 하 여 &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
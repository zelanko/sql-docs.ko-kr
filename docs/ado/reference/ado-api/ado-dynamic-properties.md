---
title: "ADO 동적 속성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fca9f032f5a72df58b18206c8441365ce3c8a746
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ado-dynamic-properties"></a>ADO 동적 속성
동적 속성에 추가할 수는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에는 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [명령](../../../ado/reference/ado-api/command-object-ado.md), 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 이러한 속성에 대 한 소스는 중 하나는 데이터 공급자와 같은 [OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), 또는 서비스 공급자와 같은 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)합니다. 적절 한 데이터 공급자 또는 특정 동적 속성에 대 한 자세한 내용은 서비스 공급자 설명서를 참조 하십시오.  
  
 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 각 표준 OLE DB provider 동적 속성에 대 한 OLE DB 및 ADO 이름 간의 상호 참조를 제공 합니다.  
  
 다음 동적 속성은 특히 흥미롭습니다 및 설명한 소스에도 문서화 되어 있습니다. ADO와 특별 한 기능 다음 목록에서 ADO 도움말 항목에서 설명 됩니다.  
  
|||  
|-|-|  
|[최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|이 필드에 인덱스를 만들지 여부를 지정 합니다.|  
|[메시지를 표시합니다](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|OLE DB 공급자에 게 초기화 정보 메시지를 표시 하는지 여부를 지정 합니다.|  
|[Name 모양 변경](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|에 대 한 이름을 지정는 **레코드 집합** 개체입니다.|  
|[다시 동기화 명령](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|지정 된 사용자가 제공한 명령 문자열의 **다시 동기화** 에 명명 된 테이블의 데이터를 새로 고치려면 메서드 문제는 **고유 테이블** 동적 속성.|  
|[고유 테이블, 고유한 스키마, 고유한 카탈로그](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**고유 테이블** 는 업데이트, 삽입 및 삭제는 사용할 수는 기본 테이블의 이름을 지정 합니다.<br /><br /> **고유한 스키마** 스키마 또는 테이블의 소유자의 이름을 지정 합니다.<br /><br /> **고유한 카탈로그** 카탈로그 또는 테이블을 포함 하는 데이터베이스의 이름을 지정 합니다.|  
|[다시 동기화를 업데이트 합니다.](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|지정 여부는 **UpdateBatch** 메서드 뒤 암시적 **다시 동기화** 메서드 작업 그리고 있다면 해당 작업의 범위입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 열거 상수](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [부록 b: ADO 오류](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 메서드](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 개체 및 인터페이스](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 속성](../../../ado/reference/ado-api/ado-properties.md)


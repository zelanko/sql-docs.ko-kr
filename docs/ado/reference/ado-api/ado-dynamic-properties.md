---
title: ADO 동적 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2ad6c2804b70011380a12b5b9e0cd1f52fd56398
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696870"
---
# <a name="ado-dynamic-properties"></a>ADO 동적 속성
동적 속성에 추가할 수 있습니다는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션의 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [명령](../../../ado/reference/ado-api/command-object-ado.md), 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 이러한 속성에 대 한 원본이 두 데이터 공급자와 같은 합니다 [OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), 또는 서비스 공급자와 같은 [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)합니다. 적절 한 데이터 공급자 또는 특정 동적 속성에 대 한 자세한 내용은 서비스 공급자 설명서를 참조 하십시오.  
  
 합니다 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 각 표준 OLE DB 공급자 동적 속성에 대 한 ADO 및 OLE DB 이름 간의 상호 참조를 제공 합니다.  
  
 다음 동적 속성 특히 흥미로운 되며 앞서 언급 한 원본에도 설명 되어 있습니다. ADO 사용 하 여 특별 한 기능 다음 목록에서 ADO 도움말 항목에 설명 되어 있습니다.  
  
|||  
|-|-|  
|[최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|이 필드에 인덱스를 만들어야 하는지 여부를 지정 합니다.|  
|[Prompt](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|OLE DB 공급자 초기화 정보에 대 한 사용자 메시지를 표시 하는지 여부를 지정 합니다.|  
|[변형 이름](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|이름을 지정 합니다 **레코드 집합** 개체입니다.|  
|[다시 동기화 명령](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|사용자가 제공한 명령 문자열을 지정 합니다 **다시 동기화** 에 지정 된 테이블에서 데이터를 새로 고치려면 메서드 문제를 **고유 테이블** 동적 속성입니다.|  
|[고유 테이블, 고유 스키마, 고유 카탈로그](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**고유 테이블** 기반이 업데이트, 삽입 및 삭제를 수행할 기본 테이블의 이름을 지정 합니다.<br /><br /> **고유한 스키마** 스키마 또는 테이블 소유자의 이름을 지정 합니다.<br /><br /> **고유 카탈로그** 카탈로그 또는 테이블이 포함 된 데이터베이스의 이름을 지정 합니다.|  
|[다시 동기화를 업데이트 합니다.](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|지정 여부는 **UpdateBatch** 메서드 뒤에 암시적 **다시 동기화** 메서드 작업 그렇다면 해당 작업의 범위.|  
  
## <a name="see-also"></a>관련 항목  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 열거 상수](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [부록 B: ADO 오류](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 메서드](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 개체 및 인터페이스](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 속성](../../../ado/reference/ado-api/ado-properties.md)

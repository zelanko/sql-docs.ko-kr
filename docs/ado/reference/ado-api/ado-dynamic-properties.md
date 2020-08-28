---
description: ADO 동적 속성
title: ADO 동적 속성 | Microsoft Docs
ms.prod: sql
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dd0186fba696d2fe3528f113bd0e07aeadd801f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976514"
---
# <a name="ado-dynamic-properties"></a>ADO 동적 속성
동적 속성을 [연결](./connection-object-ado.md), [명령](./command-object-ado.md)또는 [레코드 집합](./recordset-object-ado.md) 개체의 [속성](./properties-collection-ado.md) 컬렉션에 추가할 수 있습니다. 이러한 속성의 원본은 [SQL Server 용 OLE DB 공급자](../../guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)또는 서비스 공급자 (예: [OLE DB 용 Microsoft Cursor service](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md))와 같은 데이터 공급자입니다. 특정 동적 속성에 대 한 자세한 내용은 적절 한 데이터 공급자 또는 서비스 공급자 설명서를 참조 하십시오.  
  
 [Ado 동적 속성 인덱스](./ado-dynamic-property-index.md) 는 각 표준 OLE DB 공급자 동적 속성에 대 한 ado와 OLE DB 이름 간의 상호 참조를 제공 합니다.  
  
 다음 동적 속성은 특히 흥미롭습니다. 앞에서 설명한 원본에도 설명 되어 있습니다. ADO를 사용 하는 특수 기능은 다음 목록의 ADO 도움말 항목에 설명 되어 있습니다.  
  
|동적 속성|설명|  
|-|-|  
|[Optimize](./optimize-property-dynamic-ado.md)|이 필드에 인덱스를 만들지 여부를 지정 합니다.|  
|[프롬프트](./prompt-property-dynamic-ado.md)|OLE DB 공급자가 초기화 정보를 묻는 메시지를 사용자에 게 표시할지 여부를 지정 합니다.|  
|[이름 변경](./reshape-name-property-dynamic-ado.md)|**레코드 집합** 개체의 이름을 지정 합니다.|  
|[다시 동기화 명령](./resync-command-property-dynamic-ado.md)|**Resync** 메서드에서 **고유 테이블** 동적 속성의 테이블에 있는 데이터를 새로 고치는 데 발급 하는 사용자 제공 명령 문자열을 지정 합니다.|  
|[고유 테이블, 고유 스키마, 고유 카탈로그](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**고유 테이블** 업데이트, 삽입 및 삭제를 수행할 수 있는 기본 테이블의 이름을 지정 합니다.<br /><br /> **고유 스키마** 테이블 소유자의 스키마 또는 이름을 지정 합니다.<br /><br /> **고유 카탈로그** 테이블이 포함 된 데이터베이스의 이름 또는 카탈로그를 지정 합니다.|  
|[업데이트 다시 동기화](./update-resync-property-dynamic-ado.md)|**UpdateBatch** 메서드 뒤에 암시적 다시 **동기화** 메서드 작업이 오고 그 뒤에 해당 작업의 범위가 있는지 여부를 지정 합니다.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>참고 항목  
 [ADO API 참조](./ado-api-reference.md)   
 [ADO 컬렉션](./ado-collections.md)   
 [ADO 열거 상수](./ado-enumerated-constants.md)   
 [부록 B: ADO 오류](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](./ado-events.md)   
 [ADO 메서드](./ado-methods.md)   
 [ADO 개체 모델](./ado-object-model.md)   
 [ADO 개체 및 인터페이스](./ado-objects-and-interfaces.md)   
 [ADO 속성](./ado-properties.md)
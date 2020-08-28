---
description: ADO 개체 및 인터페이스
title: ADO 개체 및 인터페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: rothja
ms.author: jroth
ms.openlocfilehash: 80391605a0480d8967afb1e0240168a393f09363
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976314"
---
# <a name="ado-objects-and-interfaces"></a>ADO 개체 및 인터페이스
이러한 개체 간의 관계는 [ADO 개체 모델](./ado-object-model.md)에 표시 됩니다.  
  
 각 개체는 해당 컬렉션에 포함 될 수 있습니다. 예를 들어 [오류](./error-object.md) 개체는 [Errors](./errors-collection-ado.md) 컬렉션에 포함 될 수 있습니다. 자세한 내용은 [ADO 컬렉션](./ado-collections.md) 또는 특정 컬렉션 항목을 참조 하세요.  
  
|개체 또는 인터페이스|설명|  
|-|-|  
|[IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))|ADOCommand 개체에서 기본 OLEDB 명령을 검색 하는 데 사용 됩니다.|  
|[ADORecordConstruction](./adorecordconstruction-interface.md)|C/c + + 응용 프로그램의 OLE DB **Row** 개체에서 ADO **Record** 개체를 생성 합니다.|  
|[ADORecordsetConstruction](./adorecordsetconstruction-interface.md)|C/c + + 응용 프로그램의 OLE DB **Rowset** 개체에서 ADO **레코드 집합** 개체를 생성 합니다.|  
|[ADOStreamConstruction 인터페이스](./adostreamconstruction-interface.md)|C/c + + 응용 프로그램의 OLE DB **IStream** 개체에서 ADO **스트림** 개체를 생성 합니다.|  
|[명령](./command-object-ado.md)|데이터 원본에 대해 실행 하려는 특정 명령을 정의 합니다.<br /><br /> **명령** 개체는 스크립팅에 안전 하지 않습니다.|  
|[연결](./connection-object-ado.md)|데이터 소스에 대해 열려 있는 연결을 나타냅니다.<br /><br /> **연결** 개체는 스크립팅에 안전 합니다.|  
|[IDSOShapeExtensions 인터페이스](./idsoshapeextensions-interface.md)|셰이프 공급자에 대 한 기본 OLEDB 데이터 원본 개체를 가져옵니다.|  
|[오류](./error-object.md)|공급자와 관련 된 단일 작업과 관련 된 데이터 액세스 오류에 대 한 세부 정보를 포함 합니다.<br /><br /> **Error** 개체는 스크립팅에 안전 하지 않습니다.|  
|[필드](./field-object.md)|공통 데이터 형식으로 데이터의 열을 나타냅니다.|  
|[매개 변수](./parameter-object.md)|매개 변수가 있는 쿼리 또는 저장 프로시저를 기반으로 **Command** 개체와 연결 된 매개 변수 또는 인수를 나타냅니다.<br /><br /> **매개 변수** 개체는 스크립팅에 안전 하지 않습니다.|  
|[속성](./property-object-ado.md)|공급자에 의해 정의 된 ADO 개체의 동적 특성을 나타냅니다.|  
|[레코드](./record-object-ado.md)|**레코드 집합**의 행 또는 파일 시스템의 디렉터리 또는 파일을 나타냅니다. **Record** 개체는 스크립팅에 안전 합니다.|  
|[레코드 집합](./recordset-object-ado.md)|기본 테이블의 레코드 집합 또는 실행 된 명령의 결과를 나타냅니다. 언제 든 지 **레코드 집합** 개체는 집합 내의 단일 레코드만 현재 레코드로 참조 합니다.<br /><br /> **레코드 집합** 개체는 스크립팅에 안전 합니다.|  
|[스트림](./stream-object-ado.md)|데이터의 이진 스트림을 나타냅니다.<br /><br /> **Stream** 개체는 스크립팅에 안전 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ADO API 참조](./ado-api-reference.md)   
 [ADO 컬렉션](./ado-collections.md)   
 [ADO 동적 속성](./ado-dynamic-properties.md)   
 [ADO 열거 상수](./ado-enumerated-constants.md)   
 [부록 B: ADO 오류](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](./ado-events.md)   
 [ADO 메서드](./ado-methods.md)   
 [ADO 개체 모델](./ado-object-model.md)   
 [ADO 속성](./ado-properties.md)
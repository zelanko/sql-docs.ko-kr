---
title: "ADO 개체 및 인터페이스 | Microsoft Docs"
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
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d4d0b2c896be1059d999418d1f88053225c5d44a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="ado-objects-and-interfaces"></a>ADO 개체 및 인터페이스
이러한 개체 간의 관계에 표시 됩니다는 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)합니다.  
  
 각 개체는 해당 컬렉션에 포함 될 수 있습니다. 예를 들어 한 [오류](../../../ado/reference/ado-api/error-object.md) 개체에 포함 될 수는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션입니다. 자세한 내용은 참조 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md) 또는 특정 컬렉션 항목입니다.  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|기본 OLEDB 명령의 ADOCommand 개체에서 검색 하는 데 사용 합니다.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|ADO 생성 **레코드** OLE DB에서 개체 **행** C/c + + 응용 프로그램의 개체입니다.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|ADO 생성 **레코드 집합** OLE DB에서 개체 **행 집합** C/c + + 응용 프로그램의 개체입니다.|  
|[ADOStreamConstruction 인터페이스](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|ADO 생성 **스트림** OLE DB에서 개체 **IStream** C/c + + 응용 프로그램의 개체입니다.|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|데이터 원본에 대해 실행 하려는 특정 명령을 정의 합니다.<br /><br /> **명령** 개체가 스크립팅 작업에 안전 합니다.|  
|[연결](../../../ado/reference/ado-api/connection-object-ado.md)|데이터 원본에 대해 열린 연결을 나타냅니다.<br /><br /> **연결** 개체는 스크립팅 작업에 안전 합니다.|  
|[IDSOShapeExtensions 인터페이스](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|SHAPE 공급자에 대 한 기본 OLEDB 데이터 원본 개체를 가져옵니다.|  
|[오류](../../../ado/reference/ado-api/error-object.md)|공급자 관련 단일 작업에 관련 된 데이터 액세스 오류에 대 한 세부 정보를 포함 합니다.<br /><br /> **오류** 개체가 스크립팅 작업에 안전 합니다.|  
|[필드](../../../ado/reference/ado-api/field-object.md)|일반 데이터 형식과 데이터의 열을 나타냅니다.|  
|[매개 변수](../../../ado/reference/ado-api/parameter-object.md)|매개 변수 또는 연결 된 인수를 나타냅니다는 **명령** 매개 변수가 있는 쿼리 또는 저장된 프로시저에 따라 개체입니다.<br /><br /> **매개 변수** 개체가 스크립팅 작업에 안전 합니다.|  
|[속성](../../../ado/reference/ado-api/property-object-ado.md)|공급자에 의해 정의 된 ADO 개체의 동적 특성을 나타냅니다.|  
|[레코드](../../../ado/reference/ado-api/record-object-ado.md)|행을 나타냅니다는 **레코드 집합**, 디렉터리 또는 파일 시스템에는 파일입니다. **레코드** 개체는 스크립팅 작업에 안전 합니다.|  
|[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)|기본 테이블이 나 실행 된 명령의 결과에서 레코드 집합을 나타냅니다. 언제 든 지는 **레코드 집합** 개체가 현재 레코드로 집합 내에서 단일 레코드로 참조 합니다.<br /><br /> **레코드 집합** 개체는 스크립팅 작업에 안전 합니다.|  
|[스트림](../../../ado/reference/ado-api/stream-object-ado.md)|이진 데이터 스트림을 나타냅니다.<br /><br /> **스트림** 개체는 스크립팅 작업에 안전 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 동적 속성](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 열거 상수](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [부록 b: ADO 오류](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 메서드](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 속성](../../../ado/reference/ado-api/ado-properties.md)

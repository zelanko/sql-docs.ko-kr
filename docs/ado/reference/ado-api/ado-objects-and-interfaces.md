---
title: ADO 개체 및 인터페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 48b1f3794828af7f60c1d00313506fa9f9c522c8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696640"
---
# <a name="ado-objects-and-interfaces"></a>ADO 개체 및 인터페이스
이러한 개체 간의 관계가에 표시 되는 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)합니다.  
  
 각 개체는 해당 컬렉션에 포함할 수 있습니다. 예를 들어를 [오류](../../../ado/reference/ado-api/error-object.md) 개체에 포함 될 수는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md) 컬렉션입니다. 자세한 내용은 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md) 또는 특정 컬렉션 항목입니다.  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|기본 OLEDB 명령을 ADOCommand 개체에서 검색 하는 데 사용 합니다.|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|ADO 구문 **레코드** OLE DB 개체 **행** 개체 c에서 /C++ 응용 프로그램입니다.|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|ADO를 생성 **Recordset** OLE DB 개체 **행 집합** 개체 c에서 /C++ 응용 프로그램.|  
|[ADOStreamConstruction 인터페이스](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|ADO 구문 **Stream** OLE DB 개체 **IStream** 개체 c에서 /C++ 응용 프로그램입니다.|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|데이터 원본에 대해 실행 하려는 특정 명령을 정의 합니다.<br /><br /> 합니다 **명령** 개체가 스크립팅 작업에 안전 합니다.|  
|[연결](../../../ado/reference/ado-api/connection-object-ado.md)|데이터 원본에 대해 열린 연결을 나타냅니다.<br /><br /> 합니다 **연결** 개체가 스크립팅 작업에 안전 합니다.|  
|[IDSOShapeExtensions 인터페이스](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|셰이프 공급자에 대 한 내부 OLEDB 데이터 소스 개체를 가져옵니다.|  
|[오류](../../../ado/reference/ado-api/error-object.md)|공급자와 관련 된 단일 작업에 관련 된 데이터 액세스 오류에 대 한 세부 정보를 포함 합니다.<br /><br /> 합니다 **오류** 개체가 스크립팅 작업에 안전 합니다.|  
|[필드](../../../ado/reference/ado-api/field-object.md)|일반적인 데이터 형식 사용 하 여 데이터의 열을 나타냅니다.|  
|[매개 변수](../../../ado/reference/ado-api/parameter-object.md)|매개 변수 또는 연결 된 인수를 나타내는 **명령** 매개 변수가 있는 쿼리 또는 저장된 프로시저를 기반으로 개체입니다.<br /><br /> 합니다 **매개 변수** 개체가 스크립팅 작업에 안전 합니다.|  
|[속성](../../../ado/reference/ado-api/property-object-ado.md)|공급자가 정의한 ADO 개체의 동적 특성을 나타냅니다.|  
|[레코드](../../../ado/reference/ado-api/record-object-ado.md)|행을 나타냅니다는 **레코드 집합**, 디렉터리 또는 파일 시스템의 파일입니다. 합니다 **레코드** 개체가 스크립팅 작업에 안전 합니다.|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|기본 테이블 또는 실행 된 명령의 결과에서 레코드 집합을 나타냅니다. 언제 든 지 합니다 **레코드 집합** 개체를 현재 레코드로 집합 내에서 단일 레코드만 가리킵니다.<br /><br /> 합니다 **레코드 집합** 개체가 스크립팅 작업에 안전 합니다.|  
|[Stream](../../../ado/reference/ado-api/stream-object-ado.md)|이진 데이터 스트림을 나타냅니다.<br /><br /> 합니다 **Stream** 개체가 스크립팅 작업에 안전 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 동적 속성](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 열거 상수](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [부록 B: ADO 오류](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 메서드](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 속성](../../../ado/reference/ado-api/ado-properties.md)

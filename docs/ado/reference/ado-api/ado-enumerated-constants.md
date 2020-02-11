---
title: ADO 열거 상수 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a2b02498905b73f321d7585b5c91adfbfd1b4b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921027"
---
# <a name="ado-enumerated-constants"></a>ADO 열거 상수
디버깅을 지원 하기 위해 ADO 열거형에는 각 상수에 대 한 값이 나열 됩니다. 그러나이 값은 전적으로 advise 이며 ADO의 릴리스 간에 변경 될 수 있습니다. 코드는 열거 된 각 상수의 실제 값이 아닌 이름에만 의존 해야 합니다.  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|RDS **레코드 집합** 개체의 경우 데이터를 검색 하는 비동기 스레드의 실행 우선 순위를 지정 합니다.|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|**MSDataShape** 공급자가 계층적 **레코드 집합**에서 집계 열과 계산 된 열을 다시 계산 하는 시기를 지정 합니다.|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|**레코드 집합** 개체를 사용 하 여 데이터 원본 행의 낙관적 업데이트를 수행 하는 동안 충돌을 검색 하는 데 사용할 수 있는 필드를 지정 합니다.|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|**UpdateBatch** 메서드 뒤에 암시적 다시 **동기화** 메서드 작업이 오고 그 뒤에 해당 작업의 범위가 있는지 여부를 지정 합니다.|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|작업의 영향을 받는 레코드를 지정 합니다.|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|작업을 시작할 위치를 나타내는 책갈피를 지정 합니다.|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|명령 인수를 해석 하는 방법을 지정 합니다.|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|책갈피로 표시 되는 두 레코드의 상대 위치를 지정 합니다.|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|**연결**의 데이터를 수정 하거나 **레코드**를 열거나 **Record** 및 **Stream** 개체의 **Mode** 속성 값을 지정 하는 데 사용할 수 있는 권한을 지정 합니다.|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|**연결 개체** 의 **Open** 메서드가 연결이 설정 된 후에 (동기적) 또는 before (비동기적으로) 반환 되어야 하는지 여부를 지정 합니다.|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|ODBC 데이터 원본에 대 한 연결을 열 때 누락 된 매개 변수를 확인 하기 위해 대화 상자를 표시할지 여부를 지정 합니다.|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|**Copyrecord** 메서드의 동작을 지정 합니다.|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|커서 엔진의 위치를 지정 합니다.|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|에서 **지원** 되는 메서드가 테스트할 기능을 지정 합니다.|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|**레코드 집합** 개체에 사용 되는 커서의 유형을 지정 합니다.|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|**필드**, **매개 변수**또는 **속성**의 데이터 형식을 지정 합니다.|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|레코드의 편집 상태를 지정 합니다.|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|ADO 런타임 오류의 유형을 지정 합니다.|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|이벤트를 발생 시킨 이유를 지정 합니다.|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|이벤트 실행의 현재 상태를 지정 합니다.|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|공급자가 명령을 실행 하는 방법을 지정 합니다.|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|**Record** 개체의 **fields** 컬렉션에서 참조 되는 특수 필드를 지정 합니다.|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|**Field** 개체의 특성을 하나 이상 지정 합니다.|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|**필드** 개체의 상태를 지정 합니다.|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|레코드 **집합**에서 필터링 할 레코드 그룹을 지정 합니다.|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|레코드 **집합**에서 검색할 레코드 수를 지정 합니다.|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|**연결** 개체에 대 한 트랜잭션 격리 수준을 지정 합니다.|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|텍스트 **스트림** 개체에서 줄 구분 기호로 사용 되는 문자를 지정 합니다.|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|편집 하는 동안 레코드에 적용 되는 잠금 유형을 지정 합니다.|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|서버에 반환 되어야 하는 레코드를 지정 합니다.|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|**Record** 개체 **MoveRecord** 메서드의 동작을 지정 합니다.|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|개체가 열려 있는지 또는 닫혀 있는지, 데이터 원본에 연결 하 고, 명령을 실행 하거나, 데이터를 페치하는 지를 지정 합니다.|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|**매개 변수** 개체의 특성을 지정 합니다.|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|**매개** 변수가 입력 매개 변수, 출력 매개 변수 또는 둘 다를 나타내는지, 아니면 매개 변수가 저장 프로시저의 반환 값 인지를 지정 합니다.|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|**레코드 집합**을 저장할 형식을 지정 합니다.|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|레코드 **집합**내에서 레코드 포인터의 현재 위치를 지정 합니다.|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|**속성** 개체의 특성을 지정 합니다.|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|**Record** object **Open** 메서드에 기존 **레코드** 를 열지 아니면 새 **레코드** 를 만들어야 하는지를 지정 합니다.|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|**레코드**를 열기 위한 옵션을 지정 합니다. 이러한 값은 OR 연산자를 사용 하 여 결합할 수 있습니다.|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|일괄 업데이트 및 기타 대량 작업과 관련 된 레코드의 상태를 지정 합니다.|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|**Record** 개체의 유형을 지정 합니다.|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|다시 **동기화**를 호출 하 여 기본 값을 덮어쓸지 여부를 지정 합니다.|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|**스트림** 개체에서 저장할 때 파일을 만들거나 덮어쓸지 여부를 지정 합니다. 값은 AND 연산자와 함께 사용할 수 있습니다.|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|**OpenSchema** 메서드가 검색 하는 스키마 **레코드 집합** 의 유형을 지정 합니다. 레코드 **집합**내에서 레코드 검색 방향을 지정 합니다.|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|레코드 **집합**내에서 레코드 검색 방향을 지정 합니다. 실행할 **검색** 유형을 지정 합니다.|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|실행할 **검색** 유형을 지정 합니다. **Stream** 개체를 여는 옵션을 지정 합니다. 값은 AND 연산자와 함께 사용할 수 있습니다.|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|**Stream** 개체를 여는 옵션을 지정 합니다. 값은 AND 연산자와 함께 사용할 수 있습니다. **스트림** 개체에서 전체 스트림 또는 다음 줄을 읽어야 하는지 여부를 지정 합니다.|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|**스트림** 개체에서 전체 스트림 또는 다음 줄을 읽어야 하는지 여부를 지정 합니다. **스트림** 개체에 저장 된 데이터의 형식을 지정 합니다.|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|**스트림** 개체에 저장 된 데이터의 형식을 지정 합니다. 줄 구분 기호가 **스트림** 개체에 쓰여진 문자열에 추가 되는지 여부를 지정 합니다.|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|줄 구분 기호가 **스트림** 개체에 쓰여진 문자열에 추가 되는지 여부를 지정 합니다. **레코드 집합** 을 문자열로 검색할 때 형식을 지정 합니다.|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|**레코드 집합** 을 문자열로 검색할 때 형식을 지정 합니다. **Connection** 개체의 트랜잭션 특성을 지정 합니다.|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|**Connection** 개체의 트랜잭션 특성을 지정 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 동적 속성](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [부록 B: ADO 오류](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 메서드](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 개체 및 인터페이스](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 속성](../../../ado/reference/ado-api/ado-properties.md)

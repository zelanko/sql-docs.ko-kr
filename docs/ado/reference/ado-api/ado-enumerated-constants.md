---
description: ADO 열거 상수
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c2b7890cc9926025e7662e8571fb79309590f9de
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776687"
---
# <a name="ado-enumerated-constants"></a>ADO 열거 상수
디버깅을 지원 하기 위해 ADO 열거형에는 각 상수에 대 한 값이 나열 됩니다. 그러나이 값은 전적으로 advise 이며 ADO의 릴리스 간에 변경 될 수 있습니다. 코드는 열거 된 각 상수의 실제 값이 아닌 이름에만 의존 해야 합니다.  
  
|상수|설명|  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](./adcprop-asyncthreadpriority-enum.md)|RDS **레코드 집합** 개체의 경우 데이터를 검색 하는 비동기 스레드의 실행 우선 순위를 지정 합니다.|  
|[ADCPROP_AUTORECALC_ENUM](./adcprop-autorecalc-enum.md)|**MSDataShape** 공급자가 계층적 **레코드 집합**에서 집계 열과 계산 된 열을 다시 계산 하는 시기를 지정 합니다.|  
|[ADCPROP_UPDATECRITERIA_ENUM](./adcprop-updatecriteria-enum.md)|**레코드 집합** 개체를 사용 하 여 데이터 원본 행의 낙관적 업데이트를 수행 하는 동안 충돌을 검색 하는 데 사용할 수 있는 필드를 지정 합니다.|  
|[ADCPROP_UPDATERESYNC_ENUM](./adcprop-updateresync-enum.md)|**UpdateBatch** 메서드 뒤에 암시적 다시 **동기화** 메서드 작업이 오고 그 뒤에 해당 작업의 범위가 있는지 여부를 지정 합니다.|  
|[AffectEnum](./affectenum.md)|작업의 영향을 받는 레코드를 지정 합니다.|  
|[BookmarkEnum](./bookmarkenum.md)|작업을 시작할 위치를 나타내는 책갈피를 지정 합니다.|  
|[CommandTypeEnum](./commandtypeenum.md)|명령 인수를 해석 하는 방법을 지정 합니다.|  
|[CompareEnum](./compareenum.md)|책갈피로 표시 되는 두 레코드의 상대 위치를 지정 합니다.|  
|[ConnectModeEnum](./connectmodeenum.md)|**연결**의 데이터를 수정 하거나 **레코드**를 열거나 **Record** 및 **Stream** 개체의 **Mode** 속성 값을 지정 하는 데 사용할 수 있는 권한을 지정 합니다.|  
|[ConnectOptionEnum](./connectoptionenum.md)|**연결 개체** 의 **Open** 메서드가 연결이 설정 된 후에 (동기적) 또는 before (비동기적으로) 반환 되어야 하는지 여부를 지정 합니다.|  
|[ConnectPromptEnum](./connectpromptenum.md)|ODBC 데이터 원본에 대 한 연결을 열 때 누락 된 매개 변수를 확인 하기 위해 대화 상자를 표시할지 여부를 지정 합니다.|  
|[CopyRecordOptionsEnum](./copyrecordoptionsenum.md)|**Copyrecord** 메서드의 동작을 지정 합니다.|  
|[CursorLocationEnum](./cursorlocationenum.md)|커서 엔진의 위치를 지정 합니다.|  
|[CursorOptionEnum](./cursoroptionenum.md)|에서 **지원** 되는 메서드가 테스트할 기능을 지정 합니다.|  
|[CursorTypeEnum](./cursortypeenum.md)|**레코드 집합** 개체에 사용 되는 커서의 유형을 지정 합니다.|  
|[DataTypeEnum](./datatypeenum.md)|**필드**, **매개 변수**또는 **속성**의 데이터 형식을 지정 합니다.|  
|[EditModeEnum](./editmodeenum.md)|레코드의 편집 상태를 지정 합니다.|  
|[ErrorValueEnum](./errorvalueenum.md)|ADO 런타임 오류의 유형을 지정 합니다.|  
|[EventReasonEnum](./eventreasonenum.md)|이벤트를 발생 시킨 이유를 지정 합니다.|  
|[EventStatusEnum](./eventstatusenum.md)|이벤트 실행의 현재 상태를 지정 합니다.|  
|[ExecuteOptionEnum](./executeoptionenum.md)|공급자가 명령을 실행 하는 방법을 지정 합니다.|  
|[FieldEnum](./fieldenum.md)|**Record** 개체의 **fields** 컬렉션에서 참조 되는 특수 필드를 지정 합니다.|  
|[FieldAttributeEnum](./fieldattributeenum.md)|**Field** 개체의 특성을 하나 이상 지정 합니다.|  
|[FieldStatusEnum](./fieldstatusenum.md)|**필드** 개체의 상태를 지정 합니다.|  
|[FilterGroupEnum](./filtergroupenum.md)|레코드 **집합**에서 필터링 할 레코드 그룹을 지정 합니다.|  
|[GetRowsOptionEnum](./getrowsoptionenum.md)|레코드 **집합**에서 검색할 레코드 수를 지정 합니다.|  
|[IsolationLevelEnum](./isolationlevelenum.md)|**연결** 개체에 대 한 트랜잭션 격리 수준을 지정 합니다.|  
|[LineSeparatorsEnum](./lineseparatorsenum.md)|텍스트 **스트림** 개체에서 줄 구분 기호로 사용 되는 문자를 지정 합니다.|  
|[LockTypeEnum](./locktypeenum.md)|편집 하는 동안 레코드에 적용 되는 잠금 유형을 지정 합니다.|  
|[MarshalOptionsEnum](./marshaloptionsenum.md)|서버에 반환 되어야 하는 레코드를 지정 합니다.|  
|[MoveRecordOptionsEnum](./moverecordoptionsenum.md)|**Record** 개체 **MoveRecord** 메서드의 동작을 지정 합니다.|  
|[ObjectStateEnum](./objectstateenum.md)|개체가 열려 있는지 또는 닫혀 있는지, 데이터 원본에 연결 하 고, 명령을 실행 하거나, 데이터를 페치하는 지를 지정 합니다.|  
|[ParameterAttributesEnum](./parameterattributesenum.md)|**매개 변수** 개체의 특성을 지정 합니다.|  
|[ParameterDirectionEnum](./parameterdirectionenum.md)|**매개** 변수가 입력 매개 변수, 출력 매개 변수 또는 둘 다를 나타내는지, 아니면 매개 변수가 저장 프로시저의 반환 값 인지를 지정 합니다.|  
|[PersistFormatEnum](./persistformatenum.md)|**레코드 집합**을 저장할 형식을 지정 합니다.|  
|[PositionEnum](./positionenum.md)|레코드 **집합**내에서 레코드 포인터의 현재 위치를 지정 합니다.|  
|[PropertyAttributesEnum](./propertyattributesenum.md)|**속성** 개체의 특성을 지정 합니다.|  
|[RecordCreateOptionsEnum](./recordcreateoptionsenum.md)|**Record** object **Open** 메서드에 기존 **레코드** 를 열지 아니면 새 **레코드** 를 만들어야 하는지를 지정 합니다.|  
|[RecordOpenOptionsEnum](./recordopenoptionsenum.md)|**레코드**를 열기 위한 옵션을 지정 합니다. 이러한 값은 OR 연산자를 사용 하 여 결합할 수 있습니다.|  
|[RecordStatusEnum](./recordstatusenum.md)|일괄 업데이트 및 기타 대량 작업과 관련 된 레코드의 상태를 지정 합니다.|  
|[RecordTypeEnum](./recordtypeenum.md)|**Record** 개체의 유형을 지정 합니다.|  
|[ResyncEnum](./resyncenum.md)|다시 **동기화**를 호출 하 여 기본 값을 덮어쓸지 여부를 지정 합니다.|  
|[SaveOptionsEnum](./saveoptionsenum.md)|**스트림** 개체에서 저장할 때 파일을 만들거나 덮어쓸지 여부를 지정 합니다. 값은 AND 연산자와 함께 사용할 수 있습니다.|  
|[SchemaEnum](./schemaenum.md)|**OpenSchema** 메서드가 검색 하는 스키마 **레코드 집합** 의 유형을 지정 합니다. 레코드 **집합**내에서 레코드 검색 방향을 지정 합니다.|  
|[SearchDirectionEnum](./searchdirectionenum.md)|레코드 **집합**내에서 레코드 검색 방향을 지정 합니다. 실행할 **검색** 유형을 지정 합니다.|  
|[SeekEnum](./seekenum.md)|실행할 **검색** 유형을 지정 합니다. **Stream** 개체를 여는 옵션을 지정 합니다. 값은 AND 연산자와 함께 사용할 수 있습니다.|  
|[StreamOpenOptionsEnum](./streamopenoptionsenum.md)|**Stream** 개체를 여는 옵션을 지정 합니다. 값은 AND 연산자와 함께 사용할 수 있습니다. **스트림** 개체에서 전체 스트림 또는 다음 줄을 읽어야 하는지 여부를 지정 합니다.|  
|[StreamReadEnum](./streamreadenum.md)|**스트림** 개체에서 전체 스트림 또는 다음 줄을 읽어야 하는지 여부를 지정 합니다. **스트림** 개체에 저장 된 데이터의 형식을 지정 합니다.|  
|[StreamTypeEnum](./streamtypeenum.md)|**스트림** 개체에 저장 된 데이터의 형식을 지정 합니다. 줄 구분 기호가 **스트림** 개체에 쓰여진 문자열에 추가 되는지 여부를 지정 합니다.|  
|[StreamWriteEnum](./streamwriteenum.md)|줄 구분 기호가 **스트림** 개체에 쓰여진 문자열에 추가 되는지 여부를 지정 합니다. **레코드 집합** 을 문자열로 검색할 때 형식을 지정 합니다.|  
|[StringFormatEnum](./stringformatenum.md)|**레코드 집합** 을 문자열로 검색할 때 형식을 지정 합니다. **Connection** 개체의 트랜잭션 특성을 지정 합니다.|  
|[XactAttributeEnum](./xactattributeenum.md)|**Connection** 개체의 트랜잭션 특성을 지정 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ADO API 참조](./ado-api-reference.md)   
 [ADO 컬렉션](./ado-collections.md)   
 [ADO 동적 속성](./ado-dynamic-properties.md)   
 [부록 B: ADO 오류](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](./ado-events.md)   
 [ADO 메서드](./ado-methods.md)   
 [ADO 개체 모델](./ado-object-model.md)   
 [ADO 개체 및 인터페이스](./ado-objects-and-interfaces.md)   
 [ADO 속성](./ado-properties.md)
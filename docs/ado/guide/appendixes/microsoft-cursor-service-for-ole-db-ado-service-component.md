---
title: "OLE DB (ADO 서비스 구성 요소)에 대 한 Microsoft 커서 서비스 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d7a1f8568b633417196c6c9dda3e8a3615146603
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>OLE DB 개요에 대 한 Microsoft 커서 서비스
OLE DB에 대 한 Microsoft 커서 서비스의 데이터 공급자 커서 지원 기능을 보완합니다. 결과적으로 사용자에 게 기능을 모든 데이터 공급자 비교적 안정적입니다.

 커서 서비스 하면 동적 속성을 사용할 특정 메서드의 동작을 향상 시킵니다. 예를 들어는 [최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) 동적 속성와 같은 특정 작업을 용이 하 게 임시 인덱스를 만들 수는 [찾을](../../../ado/reference/ado-api/find-method-ado.md) 메서드.

 커서 서비스에는 항상에서 일괄 처리 업데이트 지원할을 수 있습니다. 또한 데이터 공급자는 정적 커서와 같은 기능이 적은 커서를 제공할 수 때 동적 커서 등 더욱 강력한 커서 유형 시뮬레이션 합니다.

## <a name="keyword"></a>키워드
 이 서비스 구성 요소를 호출 하려면 설정는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 또는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**합니다.

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>동적 속성
 다음 동적 속성에 추가 됩니다 OLE DB에 대 한 커서 서비스 호출 되 면는 **레코드 집합** 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다. 전체 목록을 **연결** 및 **레코드 집합** 개체 동적 속성에 나열 된는 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md)합니다. 연결 된 OLE DB 속성 이름은 적절 한 경우는 뒤에 포함 괄호 ADO 속성 이름입니다.

 커서 서비스 호출 된 후에 몇 가지 동적 속성을 변경 해도 기본 데이터 원본에 표시 되지 않습니다. 예를 들어 설정는 *명령 제한 시간* 속성에는 **레코드 집합** 기본 데이터 공급자에 게 표시 되지 것입니다.

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 커서 서비스 응용 프로그램에 필요한 기본 공급자의 동적 속성을 설정 할 경우 커서 서비스를 호출 하기 전에 속성을 설정 합니다. 명령 개체의 속성 설정은 항상 커서 위치에 관계 없이 원본 데이터 공급자에 전달 됩니다. 따라서 언제 든 지 속성을 설정 하려면 명령 개체도 사용할 수 있습니다.

> [!NOTE]
>  기본 데이터 공급자에서 지원 되는 경우에 동적 속성 DBPROP_SERVERDATAONINSERT 커서 서비스에서 지원 되지 않습니다.

|속성 이름|Description|
|-------------------|-----------------|
|자동 다시 계산 (DBPROP_ADC_AUTORECALC)|이 값은 얼마나 자주 나타냅니다 Data Shaping Service를 사용 하 여 만든 레코드 집합에 대 한 집계 및 계산 열이 계산 됩니다. 기본값 (값 = 1) Data Shaping Service 값이 변경 되었는지 확인 될 때마다 다시 계산 합니다. 값이 0 이면 계층을 처음으로 빌드될 때 계산 또는 집계 열만 계산 됩니다.|
|일괄 처리 크기 (DBPROP_ADC_BATCHSIZE)|데이터 저장소에 전송 되기 전에 일괄 처리할 수 있는 update 문의 수를 나타냅니다. 일괄 처리에 더 이상 문을 데이터에 더 적은 왕복을 저장합니다.|
|캐시 자식 행 (DBPROP_ADC_CACHECHILDROWS)|Data Shaping Service를 사용 하 여 만든 레코드 집합에 대 한이 값이 자식 레코드 집합이 나중에 사용할 캐시에 저장 되는지 여부를 나타냅니다.|
|커서 엔진 버전 (DBPROP_ADC_CEVER)|사용 중인 커서 서비스의 버전을 나타냅니다.|
|상태 변경 (DBPROP_ADC_MAINTAINCHANGESTATUS)를 유지 관리|여러 테이블 조인에 하나 이상의 행 다시 동기화에 사용 되는 명령 텍스트를 나타냅니다.|
|[최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|인덱스를 만들 수 있는지 여부를 나타냅니다. 로 설정 하면 **True**, 특정 작업의 실행을 개선 하기 위해 인덱스 임시 만들어 권한을 부여 합니다.|
|[Name 모양 변경](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|이름을 나타냅니다는 **레코드 집합**합니다. 현재 참조 또는 가능 후속, 데이터 셰이핑 명령 합니다.|
|[다시 동기화 명령](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|사용 되는 사용자 지정 명령 문자열을 나타냅니다는 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드 때는 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 속성은 적용 합니다.|
|[고유한 카탈로그](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|참조 하는 테이블을 포함 하는 데이터베이스의 이름을 나타냅니다는 **고유 테이블** 속성입니다.|
|[고유한 스키마](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|참조 하는 테이블의 소유자의 이름을 나타냅니다는 **고유 테이블** 속성입니다.|
|[고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|에 한 테이블의 이름을 나타냅니다는 **레코드 집합** 삽입, 업데이트 또는 삭제 하 여 수정할 수 있는 여러 테이블에서 생성 합니다.|
|업데이트 기준 (DBPROP_ADC_UPDATECRITERIA)|필드를 나타냅니다는 **여기서** 절은 업데이트 하는 동안 발생 하는 충돌을 처리 하는 데 사용 됩니다.|
|[재 동기화 업데이트](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|나타냅니다 여부는 **다시 동기화** 메서드 후 암시적으로 호출 됩니다는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드 (및 해당 동작)는 **고유 테이블** 속성은 적용 합니다.|

 설정 하거나 인덱스의 이름을 지정 하 여 동적 속성을 검색할 수도 있습니다는 **속성** 컬렉션입니다. 예를 들어 get 및 현재 값을 인쇄는 [최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) 동적 속성을 다음 새 값을 다음과 같이 설정 합니다.

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>기본 제공 속성 동작
 OLE DB에 대 한 커서 서비스는 특정 기본 제공 속성의 동작을도 영향을 줍니다.

|속성 이름|Description|
|-------------------|-----------------|
|[모두](../../../ado/reference/ado-api/cursortype-property-ado.md)|에 사용할 수 있는 커서 유형을 보완는 **레코드 집합**합니다.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|에 사용할 수 있는 잠금의 종류 보완는 **레코드 집합**합니다. 일괄 업데이트를 사용 하도록 설정 합니다.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|하나 이상의 필드에 있는 이름 지정는 **레코드 집합** 정렬 되어 각 필드가 오름차순 또는 내림차순 정렬 되 고 있는지 여부.|

## <a name="method-behavior"></a>동작 메서드
 OLE DB에 대 한 커서 서비스 사용 하거나의 동작에 영향을 [필드](../../../ado/reference/ado-api/field-object.md) 개체의 [Append](../../../ado/reference/ado-api/append-method-ado.md) 메서드가 및 **레코드 집합** 개체의 [열고](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 및 [저장](../../../ado/reference/ado-api/save-method.md) 메서드.


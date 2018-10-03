---
title: OLE DB (ADO 서비스 구성 요소)에 대 한 Microsoft 커서 서비스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c859de289a9f93a23702c63bd50269bb0881b34
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47714991"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>OLE DB 개요에 대 한 Microsoft 커서 서비스
OLE DB에 대 한 Microsoft 커서 서비스의 데이터 공급자 커서 지원 기능을 보완합니다. 결과적으로 사용자에 게 모든 데이터 공급자에서 상대적으로 균일 한 기능입니다.

 커서 서비스는 동적 속성을 사용할 수 있도록 하 고 특정 메서드의 동작을 향상 시킵니다. 예를 들어 합니다 [최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) 동적 속성와 같은 특정 작업을 용이 하 게 임시 인덱스를 만들 수는 [찾을](../../../ado/reference/ado-api/find-method-ado.md) 메서드.

 커서 서비스에는 일괄 처리 업데이트 경우도 지원할을 수 있습니다. 또한 데이터 공급자는 정적 커서와 같은 기능이 적은 커서를 제공할 수 있는 경우 동적 커서 등의 더욱 강력한 커서 유형을 시뮬레이션 합니다.

## <a name="keyword"></a>키워드
 이 서비스 구성 요소를 호출 하려면 설정 합니다 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 또는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**합니다.

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>동적 속성
 OLE DB에 대 한 커서 서비스가 호출 되 면 다음 동적 속성에 추가 됩니다는 **Recordset** 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다. 전체 목록을 **연결** 하 고 **레코드 집합** 개체의 동적 속성에 나열 됩니다는 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md)합니다. 연결된 된 OLE DB 속성의 이름은 적절 한 경우에 포함 됩니다 괄호 ADO 속성 이름 뒤에 오는.

 커서 서비스 호출 된 후에 일부 동적 속성을 변경 해도 기본 데이터 원본에 표시 되지 않습니다. 예를 들어 설정를 *명령 제한 시간* 속성을 **레코드 집합** 기본 데이터 공급자에 표시 되지 것입니다.

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 커서 서비스 응용 프로그램에 필요한 기본 공급자의 동적 속성을 설정 해야 하지만 경우에 커서 서비스를 호출 하기 전에 속성을 설정 합니다. 명령 개체 속성 설정은 항상 커서 위치에 관계 없이 기본 데이터 공급자에 전달 됩니다. 따라서 언제 든 지 속성을 설정 하려면 명령 개체를 사용할 수도 있습니다.

> [!NOTE]
>  기본 데이터 공급자가 지원 되는 경우에 동적 속성 DBPROP_SERVERDATAONINSERT 커서 서비스에서 지원 되지 않습니다.

|속성 이름|Description|
|-------------------|-----------------|
|자동 다시 계산 (DBPROP_ADC_AUTORECALC)|이 값을 얼마나 자주 나타냅니다 Data Shaping Service를 사용 하 여 만든 레코드 집합에 대 한 계산 및 집계 열이 계산 됩니다. 기본값 (값 = 1) Data Shaping Service 값이 변경 되었는지 확인 될 때마다 다시 계산 합니다. 값이 0 이면 계층을 처음으로 빌드될 때 계산 또는 집계 열만 계산 됩니다.|
|일괄 처리 크기 (DBPROP_ADC_BATCHSIZE)|데이터 저장소에 전송 되기 전에 일괄 처리할 수 있는 update 문의 수를 나타냅니다. 일괄 처리에서 더 많은 문이 데이터에 더 적은 왕복을 저장합니다.|
|캐시 자식 행 (DBPROP_ADC_CACHECHILDROWS)|Data Shaping Service를 사용 하 여 만든 레코드 집합에 대 한이 값이 자식 레코드 집합이 나중에 사용할 캐시에 저장 되는지 여부를 나타냅니다.|
|커서 엔진 버전 (DBPROP_ADC_CEVER)|사용 중인 커서 서비스의 버전을 나타냅니다.|
|상태 변경 (DBPROP_ADC_MAINTAINCHANGESTATUS)를 유지 관리|여러 테이블 조인에 하나 이상의 행 다시 동기화에 사용 되는 명령의 텍스트를 나타냅니다.|
|[최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|인덱스를 만들어야 하는지 여부를 나타냅니다. 로 설정 하면 **True**, 특정 작업의 실행을 개선 하기 위해 인덱스의 임시 생성 권한을 부여 합니다.|
|[변형 이름](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|이름을 표시 합니다 **레코드 집합**합니다. 수 현재, 참조 또는 후속 데이터 셰이핑 명령입니다.|
|[다시 동기화 명령](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|사용 되는 사용자 지정 명령 문자열을 나타냅니다는 [다시 동기화](../../../ado/reference/ado-api/resync-method.md) 메서드 때 합니다 [고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 속성이 적용 합니다.|
|[고유 카탈로그](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|참조 하는 테이블을 포함 하는 데이터베이스의 이름을 표시 합니다 **고유 테이블** 속성.|
|[고유한 스키마](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|참조 하는 테이블의 소유자의 이름을 표시 합니다 **고유 테이블** 속성.|
|[고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|에 있는 한 테이블의 이름을 나타내는 **레코드 집합** 삽입, 업데이트 또는 삭제 하 여 수정할 수 있는 여러 테이블에서 생성 합니다.|
|업데이트 기준 (DBPROP_ADC_UPDATECRITERIA)|필드를 나타내는 합니다 **여기서** 절은 업데이트 하는 동안 발생 하는 충돌을 처리 하는 데 사용 됩니다.|
|[다시 동기화 업데이트](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|나타냅니다 여부를 **다시 동기화** 후 메서드는 암시적으로 호출 됩니다는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드 (및 해당 동작) 경우는 **고유 테이블** 속성이 적용 합니다.|

 설정 하거나 인덱스 이름을 지정 하 여 동적 속성을 검색할 수도 있습니다는 **속성** 컬렉션입니다. 예를 들어, get 및 현재 값을 인쇄 합니다 [최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) 동적 속성을 다음 새 값을 다음과 같이 설정 합니다.

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>기본 제공 속성 동작
 OLE DB에 대 한 커서 서비스는 특정 기본 제공 속성의 동작을도 영향을 줍니다.

|속성 이름|Description|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|에 사용할 수 있는 커서 유형의 보완을 **레코드 집합**합니다.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|에 대 한 사용 가능한 잠금의 종류를 보완을 **레코드 집합**합니다. 일괄 업데이트를 사용 하도록 설정 합니다.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|하나 이상의 필드 이름을 지정 합니다 **레코드 집합** 정렬 각 필드가 오름차순 또는 내림차순으로 정렬 되는지 여부 및에 합니다.|

## <a name="method-behavior"></a>메서드 동작
 OLE DB에 대 한 커서를 사용 하거나의 동작에 영향을 줍니다 합니다 [필드](../../../ado/reference/ado-api/field-object.md) 개체의 [추가](../../../ado/reference/ado-api/append-method-ado.md) 메서드 및 **레코드 집합** 개체의 [엽니다](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md)를 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 및 [저장](../../../ado/reference/ado-api/save-method.md) 메서드.

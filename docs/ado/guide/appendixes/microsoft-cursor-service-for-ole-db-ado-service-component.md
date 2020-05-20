---
title: OLE DB에 대 한 Microsoft Cursor Service (ADO 서비스 구성 요소) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b0b4a3773f0de637458384e8819a7b913da3e40
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758509"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>OLE DB에 대 한 Microsoft 커서 서비스 개요
OLE DB에 대 한 Microsoft Cursor Service는 데이터 공급자의 커서 지원 기능을 보완 합니다. 따라서 사용자는 모든 데이터 공급자의 상대적으로 일관 된 기능을 제공 합니다.

 커서 서비스는 동적 속성을 사용할 수 있도록 설정 하 고 특정 메서드의 동작을 향상 시킵니다. 예를 들어 [Optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dynamic 속성을 사용 하면 임시 인덱스를 만들어 [Find](../../../ado/reference/ado-api/find-method-ado.md) 메서드와 같은 특정 작업을 쉽게 수행할 수 있습니다.

 Cursor Service를 사용 하면 모든 경우에서 일괄 업데이트를 지원할 수 있습니다. 데이터 공급자가 정적 커서와 같이 지원 되지 않는 커서만 제공할 수 있는 경우에도 동적 커서와 같은 더 강력한 커서 유형을 시뮬레이트할 수 있습니다.

## <a name="keyword"></a>키워드
 이 서비스 구성 요소를 호출 하려면 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 또는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient**로 설정 합니다.

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>동적 속성
 OLE DB에 대 한 커서 서비스가 호출 되 면 다음과 같은 동적 속성이 **레코드 집합** 개체의 [properties](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 추가 됩니다. **연결** 및 **레코드 집합** 개체 동적 속성의 전체 목록은 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md)에 나열 됩니다. 연결 된 OLE DB 속성 이름 (해당 하는 경우)은 ADO 속성 이름 뒤에 괄호 안에 포함 됩니다.

 일부 동적 속성에 대 한 변경 내용은 커서 서비스가 호출 된 후 기본 데이터 원본에 표시 되지 않습니다. 예를 들어 **레코드 집합** 에 대 한 *명령 제한 시간* 속성 설정은 기본 데이터 공급자에 게 표시 되지 않습니다.

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 응용 프로그램에 커서 서비스가 필요 하지만 기본 공급자에서 동적 속성을 설정 해야 하는 경우 커서 서비스를 호출 하기 전에 속성을 설정 합니다. 명령 개체 속성 설정은 커서 위치에 관계 없이 항상 기본 데이터 공급자에 전달 됩니다. 따라서 명령 개체를 사용 하 여 언제 든 지 속성을 설정할 수도 있습니다.

> [!NOTE]
>  기본 데이터 공급자가 지 원하는 경우에도 커서 서비스에서 동적 속성 DBPROP_SERVERDATAONINSERT를 지원 하지 않습니다.

|속성 이름|설명|
|-------------------|-----------------|
|자동 다시 계산 (DBPROP_ADC_AUTORECALC)|데이터 셰이핑 서비스를 사용 하 여 만든 레코드 집합의 경우이 값은 계산 열과 집계 열을 계산 하는 빈도를 나타냅니다. 기본값 (값 = 1)은 데이터 셰이핑 서비스에서 값이 변경 되었음을 결정할 때마다 다시 계산 하는 것입니다. 값이 0 이면 계층이 처음으로 빌드될 때만 계산 열 또는 집계 열이 계산 됩니다.|
|일괄 처리 크기 (DBPROP_ADC_BATCHSIZE)|데이터 저장소로 전송 되기 전에 일괄 처리할 수 있는 update 문의 수를 나타냅니다. 일괄 처리에 문이 많을 수록 데이터 저장소의 라운드트립이 줄어듭니다.|
|자식 행 캐시 (DBPROP_ADC_CACHECHILDROWS)|데이터 셰이핑 서비스를 사용 하 여 만든 레코드 집합의 경우이 값은 나중에 사용할 수 있도록 자식 레코드 집합을 캐시에 저장할지 여부를 나타냅니다.|
|커서 엔진 버전 (DBPROP_ADC_CEVER)|사용 중인 커서 서비스의 버전을 나타냅니다.|
|변경 상태 유지 관리 (DBPROP_ADC_MAINTAINCHANGESTATUS)|여러 테이블 조인에서 하나 이상의 행을 다시 동기화 하는 데 사용 되는 명령의 텍스트를 나타냅니다.|
|[최적화](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|인덱스를 만들어야 하는지 여부를 나타냅니다. **True**로 설정 하면 특정 작업의 실행을 향상 시키기 위해 인덱스를 임시로 만들 수 있습니다.|
|[이름 변경](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|**레코드 집합**의 이름을 나타냅니다. 현재 또는 후속 데이터 셰이핑 명령 내에서 참조할 수 있습니다.|
|[다시 동기화 명령](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|[고유 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 속성이 적용 될 때 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드에서 사용 하는 사용자 지정 명령 문자열을 나타냅니다.|
|[고유 카탈로그](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**고유 테이블** 속성에서 참조 되는 테이블을 포함 하는 데이터베이스의 이름을 나타냅니다.|
|[고유 스키마](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**고유 테이블** 속성에서 참조 되는 테이블 소유자의 이름을 나타냅니다.|
|[고유한 테이블](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|삽입, 업데이트 또는 삭제로 수정할 수 있는 여러 테이블에서 만든 **레코드 집합** 에 있는 한 테이블의 이름을 나타냅니다.|
|업데이트 조건 (DBPROP_ADC_UPDATECRITERIA)|업데이트 중에 발생 하는 충돌을 처리 하는 데 사용 되는 **where** 절의 필드를 나타냅니다.|
|[업데이트 다시 동기화](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|**고유 테이블** 속성이 적용 되는 경우 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드 (및 해당 동작) 이후에 다시 **동기화** 메서드가 암시적으로 호출 되는지 여부를 나타냅니다.|

 **속성** 컬렉션의 인덱스로 이름을 지정 하 여 동적 속성을 설정 하거나 검색할 수도 있습니다. 예를 들어 [Optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dynamic 속성의 현재 값을 가져오고 인쇄 한 후 다음과 같이 새 값을 설정 합니다.

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>기본 제공 속성 동작
 OLE DB에 대 한 Cursor Service는 특정 기본 제공 속성의 동작에도 영향을 줍니다.

|속성 이름|설명|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|**레코드 집합**에 사용할 수 있는 커서 유형을 보완 합니다.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|**레코드 집합**에 사용할 수 있는 잠금 유형을 보완 합니다. 일괄 업데이트를 사용 하도록 설정 합니다.|
|[정렬](../../../ado/reference/ado-api/sort-property.md)|**레코드 집합이** 정렬 되는 하나 이상의 필드 이름과 각 필드가 오름차순으로 정렬 되는지 또는 내림차순으로 정렬 되는지를 지정 합니다.|

## <a name="method-behavior"></a>메서드 동작
 OLE DB에 대 한 Cursor Service는 [Field](../../../ado/reference/ado-api/field-object.md) 개체의 [Append](../../../ado/reference/ado-api/append-method-ado.md) 메서드를 사용 하거나 동작에 영향을 줍니다. 그리고 **레코드 집합** 개체의 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)및 [Save](../../../ado/reference/ado-api/save-method.md) 메서드가 있습니다.

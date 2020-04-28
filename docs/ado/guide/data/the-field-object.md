---
title: Field 개체 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80e6576b236db44452c4e89b1d8f3bb8976ab120
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923981"
---
# <a name="the-field-object"></a>필드 개체
각 **필드** 개체는 일반적으로 데이터베이스 테이블의 열에 해당 합니다. 그러나 **필드** 는 챕터 라는 다른 **레코드 집합**에 대 한 포인터를 나타낼 수도 있습니다. 장 열과 같은 예외는이 가이드의 뒷부분에 설명 되어 있습니다.  
  
 **Field** 개체의 **Value** 속성을 사용 하 여 현재 레코드에 대 한 데이터를 설정 하거나 반환 합니다. 공급자가 제공 하는 기능에 따라 **필드** 개체의 일부 컬렉션, 메서드 또는 속성을 사용 하지 못할 수 있습니다.  
  
 **Field** 개체의 컬렉션, 메서드 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   **Name** 속성을 사용 하 여 필드 이름을 반환 합니다.  
  
-   **Value** 속성을 사용 하 여 필드의 데이터를 확인 하거나 변경 합니다. **Value** 는 **Field** 개체의 기본 속성입니다.  
  
-   **형식**, **전체 자릿수**및 **NumericScale** 속성을 사용 하 여 필드의 기본 특성을 반환 합니다.  
  
-   **DefinedSize** 속성을 사용 하 여 필드의 선언 된 크기를 반환 합니다.  
  
-   **ActualSize** 속성을 사용 하 여 지정 된 필드에 있는 데이터의 실제 크기를 반환 합니다.  
  
-   **Attributes** 속성 및 **속성** 컬렉션을 사용 하 여 지정 된 필드에 대해 지원 되는 기능 유형을 결정 합니다.  
  
-   **AppendChunk** 및 **GetChunk** 메서드를 사용 하 여 긴 이진 또는 긴 문자 데이터를 포함 하는 필드의 값을 조작 합니다.  
  
 공급자가 batch 업데이트를 지 원하는 경우 **Originalvalue** 및 **UnderlyingValue** 속성을 사용 하 여 일괄 처리를 업데이트 하는 동안 필드 값의 불일치를 해결 합니다.  
  
## <a name="describing-a-field"></a>필드 설명  
 다음 항목에서는 필드 개체 자체 (필드에 대 한 메타 데이터 **)를 설명** 하는 정보를 나타내는 [field](../../../ado/reference/ado-api/field-object.md) 개체의 속성에 대해 설명 합니다. 이 정보를 사용 하 여 **레코드 집합**의 스키마에 대 한 많은 정보를 확인할 수 있습니다. 이러한 속성에는 **Type**, **DefinedSize** , **ActualSize**, **Name**, **NumericScale** 및 **Precision**이 포함 됩니다.  
  
### <a name="discovering-the-data-type"></a>데이터 형식 검색  
 **Type** 속성은 필드의 데이터 형식을 나타냅니다. ADO에서 지원 되는 데이터 형식 열거 상수는 *Ado 프로그래머 참조*에서 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 에 설명 되어 있습니다.  
  
 **Adnumeric**의 부동 소수점 숫자 형식에 대 한 자세한 정보를 얻을 수 있습니다. **NumericScale** 속성은 **필드**의 값을 나타내는 데 사용 되는 소수점이 하 자릿수를 나타냅니다. **Precision** 속성은 **필드**의 값을 나타내는 데 사용 되는 최대 자릿수를 지정 합니다.  
  
### <a name="determining-field-size"></a>필드 크기 확인  
 **DefinedSize** 속성을 사용 하 여 **필드** 개체의 데이터 용량을 확인 합니다.  
  
 **ActualSize** 속성을 사용 하 여 **필드** 개체 값의 실제 길이를 반환 합니다. 모든 필드에 대해 **ActualSize** 속성은 읽기 전용입니다. ADO에서 **필드** 개체 값의 길이를 확인할 수 없는 경우 **ActualSize** 속성은 **adunknown**을 반환 합니다.  
  
 **DefinedSize** 및 **ActualSize** 속성은 다른 용도로 사용 됩니다. 예를 들어 **adVarChar** 의 선언 된 형식이 있는 **Field** 개체와 단일 문자를 포함 하는 **DefinedSize** 속성 값 50이 있다고 가정 합니다. 반환 되는 **ActualSize** 속성 값은 단일 문자의 바이트 길이입니다.  
  
### <a name="determining-field-contents"></a>필드 내용 확인  
 데이터 원본의 열 식별자는 **필드**의 **이름** 속성으로 표시 됩니다. **Field** 개체의 **Value** 속성은 필드의 실제 데이터 내용을 반환 하거나 설정 합니다. 이 속성은 기본 속성입니다.  
  
 필드의 데이터를 변경 하려면 **Value** 속성을 올바른 형식의 새 값으로 설정 합니다. 커서 유형은 업데이트를 지원 하 여 필드의 내용을 변경 해야 합니다. 일괄 처리 모드에서는 데이터베이스 유효성 검사가 수행 되지 않으므로이 경우에는 **UpdateBatch** 를 호출할 때 오류를 확인 해야 합니다. 일부 공급자는 또한 일괄 업데이트를 수행 하려고 할 때 충돌을 해결 하는 데 도움이 되는 ADO **Field** 개체의 **UnderlyingValue** 및 **originalvalue** 속성을 지원 합니다. 이러한 충돌을 해결 하는 방법에 대 한 자세한 내용은 [데이터 편집](../../../ado/guide/data/editing-data.md)을 참조 하세요.  
  
> [!NOTE]
>  레코드 집합에 새 **필드** 를 추가 **하는 경우**에는 **레코드 집합 필드** 값을 설정할 수 없습니다. 대신 새 **필드** 를 닫힌 **레코드 집합**에 추가할 수 있습니다. 그런 다음 **레코드 집합** 을 열어야 하며 이러한 **필드**에 값을 할당할 수 있습니다.  
  
### <a name="getting-more-field-information"></a>추가 필드 정보 얻기  
 ADO 개체에는 기본 제공 및 동적 속성의 두 가지 유형이 있습니다. 이 시점에서는 **Field** 개체의 기본 제공 속성만 설명 했습니다.  
  
 기본 제공 속성은 ADO에서 구현 되 고 `MyObject.Property` 구문을 사용 하 여 새 개체에서 즉시 사용할 수 있는 속성입니다. 이러한 속성은 개체의 **Properties** 컬렉션에 **속성** 개체로 표시 되지 않습니다.  
  
 동적 속성은 기본 데이터 공급자에 의해 정의 되 고 해당 ADO 개체의 **properties** 컬렉션에 표시 됩니다. 예를 들어 공급자와 관련 된 속성은 **레코드 집합** 개체가 트랜잭션을 지원 하는지 또는 업데이트를 지원 하는지 여부를 나타낼 수 있습니다. 이러한 추가 속성은 해당 **레코드 집합** 개체의 **속성** 컬렉션에 **속성** 개체로 표시 됩니다. 동적 속성은 또는 `MyObject.Properties(0)` `MyObject.Properties("Name")`구문을 사용 하 여 컬렉션을 통해서만 참조할 수 있습니다.  
  
 두 종류의 속성을 모두 삭제할 수는 없습니다.  
  
 동적 **속성** 개체에는 자체의 기본 제공 속성 4 개가 있습니다.  
  
-   **Name** 속성은 속성을 식별 하는 문자열입니다.  
  
-   **Type** 속성은 속성 데이터 형식을 지정 하는 정수입니다.  
  
-   **Value** 속성은 속성 설정을 포함 하는 변형입니다. **Value** 는 **속성** 개체의 기본 속성입니다.  
  
-   **Attributes** 속성은 공급자와 관련 된 속성의 특징을 나타내는 **Long** 값입니다.  
  
 **Field** 개체의 **Properties** 컬렉션에는 필드에 대 한 추가 메타 데이터가 포함 됩니다. 이 컬렉션의 내용은 공급자에 따라 다릅니다. 다음 코드 예제는이 섹션의 시작 부분에 도입 된 샘플 **레코드 집합** 의 **속성** 컬렉션을 검사 합니다. 먼저 컬렉션의 내용을 확인 합니다. 이 코드는 [SQL Server에 대 한 OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)를 사용 하므로 **Properties** 컬렉션에는 해당 공급자와 관련 된 정보가 포함 됩니다.  
  
```  
'BeginFieldProps  
    Dim objProp As ADODB.Property  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
  
        For Each objProp In objFields(intLoop).Properties  
            Debug.Print vbTab & objProp.Name & " = " & objProp.Value  
        Next objProp  
    Next intLoop  
'EndFieldProps  
```  
  
### <a name="dealing-with-binary-data"></a>이진 데이터 처리  
 **Field** 개체에 대해 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 메서드를 사용 하 여 긴 이진 또는 문자 데이터로 채웁니다. 시스템 메모리가 제한 된 경우에는 **AppendChunk** 메서드를 사용 하 여 전체 값이 아닌 부분에서 긴 값을 조작할 수 있습니다.  
  
 **Field** 개체의 **Attributes** 속성에서 **Adfldlong** 비트가 **True**로 설정 된 경우 해당 필드에 대해 **AppendChunk** 메서드를 사용할 수 있습니다.  
  
 **Field** 개체에 대 한 첫 번째 **AppendChunk** 호출은 필드에 데이터를 쓰고 기존 데이터를 덮어씁니다. 후속 **AppendChunk** 는 기존 데이터에 add를 호출 합니다. 한 필드에 데이터를 추가 하 고 현재 레코드의 다른 필드 값을 설정 하거나 읽는 경우 ADO는 첫 번째 필드에 데이터를 추가 하는 작업이 완료 된 것으로 가정 합니다. 첫 번째 필드에서 **AppendChunk** 메서드를 다시 호출 하는 경우 ADO는 호출을 새 **AppendChunk** 작업으로 해석 하 고 기존 데이터를 덮어씁니다. 첫 번째 **레코드 집합** 개체의 클론이 아닌 다른 **레코드 집합** 개체의 필드에 액세스 하면 **AppendChunk** 작업이 중단 되지 않습니다.  
  
 **Field** 개체에 대해 **GetChunk** 메서드를 사용 하 여 긴 이진 또는 문자 데이터의 일부 또는 전체를 검색 합니다. 시스템 메모리가 제한 된 경우에는 **GetChunk** 메서드를 사용 하 여 전체 값이 아닌 부분에서 긴 값을 조작할 수 있습니다.  
  
 **GetChunk** 호출에서 반환 하는 데이터는 *변수에*할당 됩니다. *Size* 가 나머지 데이터 보다 큰 경우 **GetChunk** 메서드는 공백이 있는 *변수* 를 사용 하지 않고 나머지 데이터만 반환 합니다. 필드가 비어 있으면 **GetChunk** 메서드는 null 값을 반환 합니다.  
  
 각 후속 **GetChunk** 호출은 이전 **GetChunk** 호출이 중단 된 위치부터 데이터를 검색 합니다. 그러나 한 필드에서 데이터를 검색 한 다음 현재 레코드의 다른 필드 값을 설정 하거나 읽는 경우 ADO는 첫 번째 필드에서 데이터 검색을 완료 했다고 가정 합니다. 첫 번째 필드에서 **GetChunk** 메서드를 다시 호출 하는 경우 ADO는 호출을 새 **GetChunk** 작업으로 해석 하 고 데이터의 시작 부분에서 읽기를 시작 합니다. 첫 번째 **레코드 집합** 개체의 클론이 아닌 다른 **레코드 집합** 개체의 필드에 액세스 하면 **GetChunk** 작업이 중단 되지 않습니다.  
  
 **Field** 개체의 **Attributes** 속성에서 **Adfldlong** 비트가 **True**로 설정 된 경우 해당 필드에 대해 **GetChunk** 메서드를 사용할 수 있습니다.  
  
 **Field** 개체에서 **GetChunk** 또는 **AppendChunk** 메서드를 사용할 때 현재 레코드가 없으면 오류 3021 (현재 레코드 없음)이 발생 합니다.  
  
 이러한 메서드를 사용 하 여 이진 데이터를 조작 하는 예제는 *ADO 프로그래머 참조*에서 [AppendChunk 메서드](../../../ado/reference/ado-api/appendchunk-method-ado.md) 및 [GetChunk 메서드](../../../ado/reference/ado-api/getchunk-method-ado.md) 예를 참조 하세요.

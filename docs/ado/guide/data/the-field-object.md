---
title: 필드 개체 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e152c3147ab7c316494c6891424c0a7c8173f002
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516530"
---
# <a name="the-field-object"></a>필드 개체
각 **필드** 개체는 일반적으로 데이터베이스 테이블의 열에 해당 합니다. 그러나를 **필드** 간에 대 한 포인터를 나타낼 수도 있습니다 **레코드 집합**, 장 이라고 합니다. 이 가이드의 뒷부분에 나오는 장 열과 같은 예외를 설명 합니다.  
  
 사용 하 여는 **값** 속성을 **필드** 개체를 설정 하거나 현재 레코드에 대 한 데이터를 반환 합니다. 기능에 따라 공급자가 제공 몇 가지 컬렉션, 메서드 또는 속성을 **필드** 개체를 사용할 수 없습니다.  
  
 컬렉션, 메서드 및 속성을 사용 하 여는 **필드** 개체를 다음을 수행할 수 있습니다.  
  
-   사용 하 여 필드의 이름을 반환 합니다 **이름을** 속성입니다.  
  
-   보거나 사용 하 여 필드의 데이터를 변경 합니다 **값** 속성입니다. **값** 의 기본 속성을 **필드** 개체입니다.  
  
-   사용 하 여 필드의 기본 특성을 반환 합니다 **형식**, **정밀도**, 및 **NumericScale** 속성입니다.  
  
-   사용 하 여 필드의 선언 된 크기를 반환 합니다 **DefinedSize** 속성입니다.  
  
-   데이터의 실제 크기를 사용 하 여 지정된 된 필드에서 반환 된 **ActualSize** 속성입니다.  
  
-   기능의 유형을 사용 하 여 지정된 된 필드에 대 한 지원 되는지 확인 합니다 **특성** 속성 및 **속성** 컬렉션입니다.  
  
-   사용 하 여 긴 이진 또는 긴 문자 데이터를 포함 하는 필드의 값을 조작 합니다 **AppendChunk** 하 고 **GetChunk** 메서드.  
  
 일괄 처리를 사용 하 여 업데이트 하는 동안 필드 값에서 불일치를 해결 합니다 **OriginalValue** 하 고 **UnderlyingValue** 속성 공급자가 지 원하는 일괄 처리 업데이트 하는 경우.  
  
## <a name="describing-a-field"></a>필드를 설명 하는  
 다음에 나오는 항목의 속성에 설명 합니다 [필드](../../../ado/reference/ado-api/field-object.md) 설명 하는 정보를 나타내는 개체를 **필드** 필드에 대 한 메타 데이터 즉, 자체 개체입니다. 이 정보는 스키마에 대해 많은 정보를 사용할 수 있습니다 합니다 **레코드 집합**합니다. 이러한 속성에 포함 **형식**, **DefinedSize** 하 고 **ActualSize**를 **이름**, 및 **NumericScale**하 고 **정밀도**합니다.  
  
### <a name="discovering-the-data-type"></a>데이터 형식 검색  
 합니다 **형식** 속성 필드의 데이터 형식을 나타냅니다. ADO에서 지원 되는 열거 상수에 설명 된 데이터 형식을 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 에 *ADO 프로그래머 참고 자료*합니다.  
  
 부동 소수점 숫자 형식 등 **adNumeric**, 자세한 정보를 얻을 수 있습니다. 합니다 **NumericScale** 속성 값을 나타내는 소수점 오른쪽 자릿수 사용할 것임을 나타냅니다 합니다 **필드**합니다. 합니다 **정밀도** 속성에 대 한 값을 나타내는 데 사용 되는 숫자의 최대 수를 지정 합니다 **필드**합니다.  
  
### <a name="determining-field-size"></a>필드 크기를 결정합니다.  
 사용 된 **DefinedSize** 속성의 데이터 용량을 확인 하는 **필드** 개체.  
  
 사용 합니다 **ActualSize** 의 실제 길이 반환 하도록 속성을 **필드** 개체의 값입니다. 모든 필드에는 **ActualSize** 속성은 읽기 전용입니다. ADO의 길이 확인할 수 없는 경우는 **필드** 개체의 값을 **ActualSize** 속성에서 반환 **adUnknown**합니다.  
  
 **DefinedSize** 하 고 **ActualSize** 속성에는 다른 목적으로 합니다. 예를 들어를 **필드** 개체의 선언 형식과 **집합이 있으므로 필요** 와 **DefinedSize** 50으로 단일 문자가 포함 된 속성 값입니다. 합니다 **ActualSize** 반환 하는 속성 값이 단일 문자의 길이 (바이트)에서입니다.  
  
### <a name="determining-field-contents"></a>필드 내용 확인  
 데이터 원본에서 열 id가 나타내는 합니다 **이름** 의 속성을 **필드**합니다. 합니다 **값** 의 속성을 **필드** 개체를 반환 하거나 필드의 실제 데이터 콘텐츠를 설정 합니다. 기본 속성입니다.  
  
 필드의 데이터를 변경 하려면 설정 합니다 **값** 속성이 올바른 형식의 새 값입니다. 커서 유형에 필드의 콘텐츠를 변경 하는 업데이트를 지원 해야 합니다. 데이터베이스 유효성 검사가 수행 되지 않으므로 여기 일괄 처리 모드에서 호출 하는 경우 오류를 확인 해야 합니다 **UpdateBatch** 이러한 경우입니다. 일부 공급자는 ADO 기능도 **필드** 개체의 **UnderlyingValue** 하 고 **OriginalValue** 지원 하려고 할 때 충돌을 해결 하기 위해 속성 일괄 처리 업데이트를 수행 합니다. 이러한 충돌을 해결 하는 방법에 대 한 자세한 내용은 참조 하세요 [데이터 편집](../../../ado/guide/data/editing-data.md)합니다.  
  
> [!NOTE]
>  **레코드 집합 필드** 새로 추가 하는 경우 값을 설정할 수 없습니다 **필드** 에 **Recordset**합니다. 대신, 새 **필드** 닫힌에 **레코드 집합**합니다. 그런 다음 **Recordset** 열린, 한 다음 수 값 할당 받아야 이러한 **필드**합니다.  
  
### <a name="getting-more-field-information"></a>더 많은 필드 정보 가져오기  
 ADO 개체에는 두 가지 유형의 속성: 기본 제공 및 동적입니다. 이 지점으로의 기본 속성만 합니다 **필드** 개체 설명 했습니다.  
  
 기본 제공 속성은 이러한 ado에서 구현 하 고 즉시 사용할 수 있는 새 개체 속성을 사용 하 여는 `MyObject.Property` 구문입니다. 로 표시 되지 않습니다 **속성** 개체의 개체 **속성** 컬렉션입니다.  
  
 동적 속성은 기본 데이터 공급자가 정의 되 고에 표시 합니다 **속성** 적절 한 ADO 개체의 컬렉션입니다. 경우 공급자에 게 특정 속성을 나타낼 수 있습니다 예를 들어를 **레코드 집합** 트랜잭션이나 업데이트 개체를 지원 합니다. 이러한 추가 속성으로 나타납니다 **속성** 하는 개체 **Recordset** 개체의 **속성** 컬렉션입니다. 동적 속성 구문을 사용 하 여 컬렉션을 통해서만 참조할 수 있습니다 `MyObject.Properties(0)` 또는 `MyObject.Properties("Name")`합니다.  
  
 두 가지 속성을 삭제할 수 없습니다.  
  
 동적 **속성** 개체에는 자체의 네 가지 기본 제공 속성:  
  
-   합니다 **이름을** 속성은 속성을 식별 하는 문자열입니다.  
  
-   합니다 **형식** 속성은 속성 데이터 형식을 지정 하는 정수입니다.  
  
-   합니다 **값** 속성이 속성 설정이 포함 된 변형입니다. **값** 에 대 한 기본 속성을 **속성** 개체입니다.  
  
-   **특성** 속성이 **긴** 공급자와 관련 속성의 특성을 나타내는 값입니다.  
  
 합니다 **속성** 컬렉션에 대 한 합니다 **필드** 필드에 대 한 추가 메타 데이터를 포함 하는 개체입니다. 이 컬렉션의 콘텐츠 공급자에 따라 달라 집니다. 다음 코드 예제를 검사 합니다 **속성** 샘플의 컬렉션 **레코드 집합** 이 섹션의 시작 부분에 도입 합니다. 먼저 컬렉션의 내용을 찾습니다. 이 코드를 사용 합니다 [OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)이므로 **속성** 컬렉션에 해당 공급자와 관련 된 정보가 포함 되어 있습니다.  
  
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
  
### <a name="dealing-with-binary-data"></a>이진 데이터로 처리합니다.  
 사용 합니다 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 메서드를 **필드** 긴 이진 또는 문자 데이터로 채울 개체입니다. 시스템 메모리가 제한 된 상황에서 사용할 수 있습니다 합니다 **AppendChunk** 부분에서 아니라 온전히에서 long 값을 조작 하는 방법입니다.  
  
 경우는 **adFldLong** 비트를 **특성** 속성을 **필드** 개체로 설정 됩니다 **True**, 사용할 수는  **AppendChunk** 해당 필드에 대 한 메서드.  
  
 첫 번째 **AppendChunk** 호출을 **필드** 모든 기존 데이터를 덮어쓰지 개체 필드 데이터를 씁니다. 후속 **AppendChunk** 호출 기존 데이터를 추가 합니다. 하나의 필드에 데이터를 추가 하 고 설정 하거나 현재 레코드의 다른 필드의 값을 읽은 다음, ADO는 완성 된 데이터의 첫 번째 필드를 추가 한다고 가정 합니다. 호출 하는 경우는 **AppendChunk** 새 호출을 해석 하는 첫 번째 필드에 다시 ADO 메서드 **AppendChunk** 작업 하 고 기존 데이터를 덮어씁니다. 다른 필드에 액세스할 **Recordset** 첫 번째 복제 되지 않은 개체 **레코드 집합** 개체에 영향을 주지 **AppendChunk** 작업 합니다.  
  
 사용 하 여 합니다 **GetChunk** 메서드를 **필드** 긴 이진 또는 문자 데이터의 일부 또는 전체를 검색할 개체입니다. 시스템 메모리가 제한 된 상황에서 사용할 수 있습니다 합니다 **GetChunk** 부분을 대신 전체적으로 긴 값을 조작 하는 방법입니다.  
  
 데이터는 한 **GetChunk** 호출 반환에 할당 된 *변수*합니다. 하는 경우 *크기* 나머지 데이터를 보다는 **GetChunk** 메서드 패딩 나머지 데이터만 반환 *변수* 빈 공간을 사용 하 여 합니다. 필드가 비어 있으면 합니다 **GetChunk** 메서드는 null 값을 반환 합니다.  
  
 각 후속 **GetChunk** 위치에서 시작 하는 데이터를 검색 하는 호출 이전 **GetChunk** 호출을 중단 합니다. 그러나 필드의 데이터를 검색 하 고 설정한 또는 현재 레코드의 다른 필드의 값을 읽을 경우 ADO 첫 번째 필드에서 데이터를 검색 하는 것이 마친 가정 합니다. 호출 하는 경우는 **GetChunk** 새 호출을 해석 하는 첫 번째 필드에 다시 ADO 메서드 **GetChunk** 작업 및 데이터의 시작 부분에서 읽기 시작 합니다. 다른 필드에 액세스할 **Recordset** 첫 번째 복제 되지 않은 개체 **레코드 집합** 개체에 영향을 주지 **GetChunk** 작업 합니다.  
  
 경우는 **adFldLong** 비트를 **특성** 속성을 **필드** 개체로 설정 됩니다 **True**, 사용할 수는 **GetChunk**  해당 필드에 대 한 메서드.  
  
 사용 하는 경우 현재 레코드가 없는 경우는 **GetChunk** 또는 **AppendChunk** 메서드를 **필드** 개체 3021 (현재 레코드 없음) 오류가 발생 합니다.  
  
 이러한 메서드를 사용 하 여 이진 데이터를 조작 하는 예제를 보려면 합니다 [AppendChunk 메서드](../../../ado/reference/ado-api/appendchunk-method-ado.md) 및 [GetChunk 메서드](../../../ado/reference/ado-api/getchunk-method-ado.md) 예제의 합니다 *ADO 프로그래머 참고 자료*합니다.

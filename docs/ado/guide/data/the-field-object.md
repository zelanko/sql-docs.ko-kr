---
title: "Field 개체 | Microsoft Docs"
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
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1f3d141fc218101902ae094ff2a4db385d204fa3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="the-field-object"></a>Field 개체
각 **필드** 개체는 일반적으로 데이터베이스 테이블의 열에 해당 합니다. 그러나 한 **필드** 다른에 대 한 포인터를 나타낼 수도 있습니다 **레코드 집합**, 장 이라고 합니다. 이 가이드의 뒷부분에 나오는 장 열과 같은 예외를 설명 합니다.  
  
 사용 하 여는 **값** 속성 **필드** 개체를 설정 하거나 현재 레코드에 대 한 데이터를 반환 합니다. 기능에 따라 공급자가 제공 컬렉션, 메서드 또는 속성의 일부는 **필드** 개체를 사용할 수 없습니다.  
  
 컬렉션, 메서드 및 속성의는 **필드** 개체를 다음을 수행할 수 있습니다.  
  
-   필드의 이름을 사용 하 여 반환 된 **이름** 속성입니다.  
  
-   보기 또는 필드의 데이터를 사용 하 여 변경 된 **값** 속성입니다. **값** 은의 기본 속성은 **필드** 개체입니다.  
  
-   필드의 기본 특성을 사용 하 여 반환 된 **형식**, **정밀도**, 및 **NumericScale** 속성.  
  
-   필드의 선언 된 크기를 사용 하 여 반환 된 **DefinedSize** 속성입니다.  
  
-   지정된 된 필드에는 데이터의 실제 크기를 사용 하 여 반환 된 **ActualSize** 속성입니다.  
  
-   사용 하 여 특정된 필드에 어떤 종류의 기능 지원 되는지 확인은 **특성** 속성 및 **속성** 컬렉션입니다.  
  
-   사용 하 여 긴 이진 또는 긴 문자 데이터를 포함 하는 필드의 값을 조작는 **AppendChunk** 및 **GetChunk** 메서드.  
  
 일괄 처리를 사용 하 여 업데이트 하는 동안 필드 값에서 불일치를 해결할는 **OriginalValue** 및 **UnderlyingValue** 속성, 공급자가 지 원하는 일괄 업데이트 합니다.  
  
## <a name="describing-a-field"></a>필드를 설명 하는  
 가 다음에 나오는 항목의 속성을 설명는 [필드](../../../ado/reference/ado-api/field-object.md) 설명 하는 정보를 나타내는 개체는 **필드** 개체 자체-즉, 메타 데이터 필드에 대 한 합니다. 스키마에 대 한 많은 정보는이 정보를 사용할 수 있습니다는 **레코드 집합**합니다. 이러한 속성에는 **형식**, **DefinedSize** 및 **ActualSize**, **이름**, 및 **NumericScale**및 **정밀도**합니다.  
  
### <a name="discovering-the-data-type"></a>데이터 형식 확인  
 **형식** 속성 필드의 데이터 형식을 나타냅니다. ADO에서 지원 되는 열거 상수에 설명 된 데이터 형식 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 에 *ADO Programmer's Reference*합니다.  
  
 부동 소수점 숫자 형식 등 **adNumeric**, 자세한 정보를 얻을 수 있습니다. **NumericScale** 속성에 대 한 값을 나타내는 소수점 오른쪽 자릿수는 나타냅니다는 **필드**합니다. **정밀도** 속성 지정에 대 한 값을 나타내는 데 사용 되는 최대 자릿수는 **필드**합니다.  
  
### <a name="determining-field-size"></a>필드 크기 확인  
 사용 하 여는 **DefinedSize** 속성의 데이터 용량을 확인 하는 **필드** 개체입니다.  
  
 사용 하 여는 **ActualSize** 의 실제 길이 반환 하는 **필드** 개체의 값입니다. 모든 필드에는 **ActualSize** 속성은 읽기 전용입니다. ADO의 길이 확인할 수 없는 경우는 **필드** 개체의 값은 **ActualSize** 속성에서 반환 **adUnknown**합니다.  
  
 **DefinedSize** 및 **ActualSize** 속성에는 다른 목적으로 합니다. 예를 들어 한 **필드** 개체의 선언 된 형식과 **집합이 있으므로 필요** 및 **DefinedSize** 50으로 단일 문자를 포함 하는 속성 값입니다. **ActualSize** 반환 하는 속성 값은 단일 문자 길이 (바이트)에서입니다.  
  
### <a name="determining-field-contents"></a>필드 내용 확인  
 데이터 원본의 열 식별자도 표시 됩니다는 **이름** 의 속성은 **필드**합니다. **값** 의 속성은 **필드** 개체를 반환 하거나 필드의 실제 데이터 내용을 설정 합니다. 기본 속성입니다.  
  
 필드의 데이터를 변경 하려면 설정는 **값** 속성에 올바른 형식의 새 값입니다. 커서 유형에 필드의 내용을 변경에 대 한 업데이트를 지원 해야 합니다. 데이터베이스 유효성 검사가 수행 되지 않으므로 여기 일괄 처리 모드에서 호출 하는 경우 오류를 확인 해야 합니다 **UpdateBatch** 이러한 경우입니다. 일부 공급자는 또한 ADO 지원 **필드** 개체의 **UnderlyingValue** 및 **OriginalValue** 하려고 할 때 충돌 해결에 도움이 되는 속성 일괄 처리 업데이트를 수행 합니다. 이러한 충돌을 해결 하는 방법에 대 한 세부 정보를 참조 하십시오. [데이터 편집](../../../ado/guide/data/editing-data.md)합니다.  
  
> [!NOTE]
>  **레코드 집합 필드** 새로운를 추가할 때 값을 설정할 수 없습니다 **필드** 에 **레코드 집합**합니다. 대신, 새 **필드** ा ए 닫힌에 **레코드 집합**합니다. 그런 다음 **레코드 집합** 열었다 다음 수 값 수에 할당 해야 이러한 **필드**합니다.  
  
### <a name="getting-more-field-information"></a>추가 필드 정보 얻기  
 ADO 개체에는 두 가지 유형의 속성: 기본 제공 및 동적입니다. 기본 제공 속성에만이 지점에는 **필드** 개체 설명 했습니다.  
  
 기본 제공 속성은 즉시 사용할 수 및 ADO에서 구현 된 이러한 속성 new를 사용 하 여 개체는 `MyObject.Property` 구문입니다. 으로 표시 되지 않는 **속성** 개체는 개체의 **속성** 컬렉션입니다.  
  
 동적 속성은 기본 데이터 공급자에 의해 정의 되며에 표시 된 **속성** 해당 ADO 개체에 대 한 컬렉션입니다. 예를 들어 한 속성 공급자와 관련 수를 표시 하는 경우는 **레코드 집합** 개체가 트랜잭션이나 업데이트를 지원 합니다. 이러한 추가 속성으로 나타납니다. **속성** 개체에 있는 **레코드 집합** 개체의 **속성** 컬렉션입니다. 동적 속성 구문을 사용 하는 컬렉션을 통해만 참조할 수 `MyObject.Properties(0)` 또는 `MyObject.Properties("Name")`합니다.  
  
 두 가지 속성을 삭제할 수 없습니다.  
  
 동적 **속성** 개체에는 자체의 네 가지 기본 제공 속성:  
  
-   **이름** 속성은 속성을 식별 하는 문자열입니다.  
  
-   **형식** 속성은 속성 데이터 형식을 지정 하는 정수입니다.  
  
-   **값** 속성은 속성 설정을 포함 하는 variant입니다. **값** 은 대 한 기본 속성을 **속성** 개체입니다.  
  
-   **특성** 속성은 한 **긴** 공급자와 관련 된 속성의 특징을 나타내는 값입니다.  
  
 **속성** 에 대 한 컬렉션은 **필드** 개체 필드에 대 한 추가 메타 데이터를 포함 합니다. 이 컬렉션의 콘텐츠 공급자에 따라 달라 집니다. 다음 코드 예제에서는 검사 하는 **속성** 샘플의 컬렉션 **레코드 집합** 이 섹션의 시작 부분에서 도입 되었습니다. 컬렉션의 내용에서 먼저 찾습니다. 사용 하 여이 코드는 [OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)이므로 **속성** 컬렉션에 해당 공급자와 관련 된 정보가 포함 되어 있습니다.  
  
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
 사용 하 여는 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 에서 메서드는 **필드** 긴 이진 또는 문자 데이터로 채울 개체입니다. 시스템 메모리가 제한 된 상황에서 사용할 수 있습니다는 **AppendChunk** 메서드 긴 값으로 아니라 전체에서를 합니다.  
  
 경우는 **adFldLong** 비트는 **특성** 속성의는 **필드** 개체로 설정 되어 **True**, 사용할 수 있습니다는 ** AppendChunk** 해당 필드에 대 한 메서드.  
  
 첫 번째 **AppendChunk** 에서 호출 된 **필드** 기존 데이터 덮어쓰기 개체 필드를 데이터를 씁니다. 후속 **AppendChunk** 호출 기존 데이터에 추가 합니다. 한 필드를 데이터를 추가 하 고 다음을 설정 하거나 현재 레코드의 다른 필드의 값을 읽을 경우 ADO 완료 데이터 첫 번째 필드를 추가 한다고 가정 합니다. 호출 하는 경우는 **AppendChunk** 첫 번째 필드에 다시 ADO 1 보다 크거나 새 호출 **AppendChunk** 작업 하 고 기존 데이터를 덮어씁니다. 다른 필드에 액세스 **레코드 집합** 첫 번째 복제본 없는 개체가 **레코드 집합** 개체에 영향을 주지 **AppendChunk** 작업 합니다.  
  
 사용 하 여는 **GetChunk** 에서 메서드는 **필드** 긴 이진 또는 문자 데이터의 일부 또는 전체를 검색 하는 개체입니다. 시스템 메모리가 제한 된 상황에서 사용할 수 있습니다는 **GetChunk** 메서드,으로 아니라 전체에서 긴 값을 조작 합니다.  
  
 데이터를 한 **GetChunk** 호출이 반환에 할당 된 *변수*합니다. 경우 *크기* 나머지 데이터를 보다 크면는 **GetChunk** 메서드 패딩 없이 나머지 데이터만 반환 *변수* 빈 공백을 사용 하 여 합니다. 필드가 비어 있으면는 **GetChunk** 메서드는 null 값을 반환 합니다.  
  
 각 후속 **GetChunk** 어디에서 시작 하는 데이터를 검색 하는 호출 이전 **GetChunk** 호출을 중단 합니다. 그러나 한 필드의 데이터를 검색 하 고 다음을 설정 하거나 현재 레코드의 다른 필드의 값을 읽을 경우 ADO 첫 번째 필드에서 데이터를 검색 했으면 가정 합니다. 호출 하는 경우는 **GetChunk** 첫 번째 필드에 다시 ADO 1 보다 크거나 새 호출 **GetChunk** 작업과 데이터의 시작 부분에서 읽기 시작 합니다. 다른 필드에 액세스 **레코드 집합** 첫 번째 복제본 없는 개체가 **레코드 집합** 개체에 영향을 주지 **GetChunk** 작업 합니다.  
  
 경우는 **adFldLong** 비트는 **특성** 속성의는 **필드** 개체로 설정 되어 **True**, 사용할 수 있습니다는 **GetChunk ** 해당 필드에 대 한 메서드.  
  
 사용 하는 경우 현재 레코드가 없는 경우는 **GetChunk** 또는 **AppendChunk** 에서 메서드는 **필드** 개체 3021 (현재 레코드 없음) 오류가 발생 합니다.  
  
 이러한 메서드를 사용 하 여 이진 데이터를 조작 하는 예제를 보려면는 [AppendChunk 메서드](../../../ado/reference/ado-api/appendchunk-method-ado.md) 및 [GetChunk 메서드](../../../ado/reference/ado-api/getchunk-method-ado.md) 의 예제는 *ADO Programmer's Reference*합니다.

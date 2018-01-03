---
title: "Append 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _DynaCollection::Append
helpviewer_keywords: Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d0c0c887da52e8c91caeab582c2b1973b491e81d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="append-method-ado"></a>Append 메서드 (ADO)
컬렉션에 개체를 추가합니다. 컬렉션의 경우 [필드](../../../ado/reference/ado-api/fields-collection-ado.md), 새 [필드](../../../ado/reference/ado-api/field-object.md) 컬렉션에 추가 하기 전에 개체를 만들 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>매개 변수  
 *컬렉션*  
 컬렉션 개체입니다.  
  
 *필드*  
 A **필드** 컬렉션입니다.  
  
 *개체*  
 개체 변수 추가 되는 개체를 나타내는입니다.  
  
 *이름*  
 A **문자열** 새 이름을 포함 하는 값 **필드** 개체를 아니어야 이름이 같은 다른 개체에서 *필드*합니다.  
  
 *형식*  
 A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 값, 기본값은 **adEmpty**, 새 필드의 데이터 형식을 지정 하는 합니다. ADO에서 다음 데이터 형식은 지원 되지 않습니다 및 해야 하지 될 경우 사용된 추가 새 필드를 한 [Recordset 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**, **adIUnknown**, **adVariant**합니다.  
  
 *DefinedSize*  
 (선택 사항) A **긴** 문자 또는 바이트 새 필드의 정의 된 크기를 나타내는 값입니다. 이 매개 변수에 대 한 기본 값에서 파생 됩니다 *형식*합니다. 이 있는 필드는 *DefinedSize* 가변 길이 열으로 처리 됩니다 255 바이트 보다 큰 값입니다. 에 대 한 기본 *DefinedSize* 지정 되지 않았습니다.  
  
 *Attrib*  
 (선택 사항) A [파생](../../../ado/reference/ado-api/fieldattributeenum.md) 값, 기본값은 **adFldDefault**, 새 필드에 대 한 특성을 지정 하는 합니다. 이 값을 지정 하지 않으면을 가질 수에서 파생 된 특성 *형식*합니다.  
  
 *FieldValue*  
 (선택 사항) A **Variant** 새 필드의 값을 나타내는입니다. 지정 하지 않으면 값이 null 인 필드가 추가 됩니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="parameters-collection"></a>Parameters 컬렉션  
 설정 해야 합니다는 [형식](../../../ado/reference/ado-api/type-property-ado.md) 속성은 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체에 추가 하기 전에 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다. 가변 길이 데이터 형식을 선택 하는 경우 설정 해야는 [크기](../../../ado/reference/ado-api/size-property-ado-parameter.md) 속성을 0 보다 큰 값입니다.  
  
 사용자가 직접 매개 변수를 설명 하는 공급자에 대 한 호출을 최소화 하 고 저장된 프로시저 또는 매개 변수가 있는 쿼리를 사용 하는 경우 성능이 향상 됩니다 합니다. 그러나 저장된 프로시저와 관련 된 또는 호출 하려는 쿼리 매개 변수가 있는 매개 변수 속성을 알고 있어야 합니다.  
  
 사용 하 여는 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 를 만들 방법을 **매개 변수** 적절 한 속성 설정 및 사용 하 여 사용 하 여 개체는 **Append** 메서드를 추가 하는 [ 매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다. 이 설정 하 고 매개 변수 정보에 대 한 공급자를 호출 하지 않고 매개 변수 값을 반환할 수 있습니다. 수동으로를 채우는이 메서드를 사용 해야 매개 변수 정보를 제공 하지 않는 공급자를 작성 하는 경우는 **매개 변수** 전혀 매개 변수를 사용 하기 위해 컬렉션입니다.  
  
## <a name="fields-collection"></a>Fields 컬렉션  
 *FieldValue* 추가 하는 경우에 매개 변수는 유효한만 **필드** 개체를 한 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 아니라 개체는 **레코드 집합** 개체입니다. 와 **레코드** 개체 필드를 추가 하 고 동시에 값을 제공할 수 있습니다. 와 **레코드 집합** 개체를 하는 동안 필드를 만들어야 합니다는 **레코드 집합** , 닫혀 있고 연 다음는 **레코드 집합** 필드에 값을 할당 하 고 있습니다.  
  
> [!NOTE]
>  새 **필드** 에 추가 된 개체는 **필드** 의 컬렉션을 **레코드** 개체는 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성을 설정 해야 다른 모든 하기 전에 **필드** 속성을 지정할 수 있습니다. 먼저, 특정 값에 대 한는 **값** 속성이 할당 해야 하 고 [업데이트](../../../ado/reference/ado-api/update-method.md) 에 **필드** 이라는 컬렉션. 그런 다음 같은 다른 속성과 [형식](../../../ado/reference/ado-api/type-property-ado.md) 또는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 액세스할 수 있습니다. **필드** 다음 데이터 형식의 개체 (**DataTypeEnum**)에 추가할 수 없습니다는 **필드** 컬렉션 되려면 오류가 발생 합니다: **adArray**, **adChapter**, **adEmpty**, **adPropVariant**, 및 **adUserDefined**합니다. 또한, 다음 데이터 형식은 ADO에서 지원 되지 않습니다: **adIDispatch**, **adIUnknown**, 및 **adIVariant**합니다. 이러한 형식에 대 한 추가할 때 오류가 발생 하지만 사용 메모리 누수와 같은 예기치 않은 결과 생성할 수 있습니다.  
  
## <a name="recordset"></a>레코드 집합  
 설정 하지 않은 경우는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 호출 하기 전에 속성에서 **Append** 메서드를 **앞** 로 설정 됩니다 **adUseClient** ( [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) 값) 될 때 자동으로 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 의 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 호출 합니다.  
  
 런타임 오류가 발생 합니다는 **추가** 메서드가 호출 되는 **필드** 열린 컬렉션 **레코드 집합**, 또는 **레코드 집합** 여기서는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성이 설정 되어 있습니다. 필드에만 추가할 수 있습니다는 **레코드 집합** 열려 있지 않으면 하 고 데이터 원본에 아직 연결 되지 않은 합니다. 이 경우 일반적으로 때는 **레코드 집합** 개체와 위조 됩니다는 [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) 메서드 또는 개체 변수에 할당 합니다.  
  
## <a name="record"></a>레코드  
 경우 런타임 오류가 발생 하지 것입니다는 **Append** 메서드가 호출 되는 **필드** 열린 컬렉션 **레코드**합니다. 새 필드에 추가 됩니다는 **필드** 의 컬렉션은 **레코드** 개체입니다. 경우는 **레코드** 에서 파생 된는 **레코드 집합**, 새 필드에 표시 되지 것입니다는 **필드** 의 컬렉션은 **레코드 집합** 개체입니다.  
  
 존재 하지 않는 필드를 작성 및에 추가 된 **필드** 컬렉션에 이미 존재 하는 경우 필드 개체에 값을 할당 하 여 컬렉션입니다. 할당 작업은 자동 생성 및의 추가 트리거한는 **필드** 개체를 할당 한 다음 완료 됩니다.  
  
 추가 후는 **필드** 에 **필드** 의 컬렉션은 **레코드** 개체를 호출 하는 **업데이트** 의 메서드는 **필드**  컬렉션의 변경 내용을 저장 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
- [Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [추가 및 CreateParameter 메서드 예제 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [추가 및 CreateParameter 메서드 예제 (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO Parameters 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)

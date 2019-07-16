---
title: Append 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 17fa0ff30e8dcdbf7ea67080f17c3e066bba8605
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920667"
---
# <a name="append-method-ado"></a>Append 메서드(ADO)
컬렉션에 개체를 추가합니다. 컬렉션이 [필드](../../../ado/reference/ado-api/fields-collection-ado.md), 새 [필드](../../../ado/reference/ado-api/field-object.md) 컬렉션에 추가 하기 전에 개체를 만들 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>매개 변수  
 *collection*  
 컬렉션 개체입니다.  
  
 *fields*  
 A **필드** 컬렉션입니다.  
  
 *object*  
 추가할 개체를 나타내는 개체 변수입니다.  
  
 *이름*  
 A **문자열** 의 새 이름을 포함 하는 값 **필드** 개체를 아니어야 이름이 같은 다른 개체에 *필드*합니다.  
  
 *형식*  
 A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 값을 해당 기본값은 **adEmpty**, 새 필드의 데이터 형식을 지정 하는 합니다. 데이터 형식은 ADO에서 지원 되지 않으며 해야 하지 수 사용 되는 경우 새 필드 추가에 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**하십시오 **adIUnknown**, **adVariant**합니다.  
  
 *DefinedSize*  
 (선택 사항) A **긴** 문자 또는 바이트, 새 필드의 정의 된 크기를 나타내는 값입니다. 이 매개 변수에 대 한 기본 값에서 파생 됩니다 *형식*합니다. 있는 필드를 *DefinedSize* 보다 255 바이트 가변 길이 열으로 처리 됩니다. 에 대 한 기본 *DefinedSize* 지정 되지 않았습니다.  
  
 *Attrib*  
 (선택 사항) A [파생](../../../ado/reference/ado-api/fieldattributeenum.md) 값을 해당 기본값은 **adFldDefault**, 새 필드의 특성을 지정 하는 합니다. 이 값을 지정 하지 않으면 하는 경우 필드에서 파생 된 특성에 포함 됩니다 *형식*합니다.  
  
 *FieldValue*  
 (선택 사항) A **Variant** 새 필드의 값을 나타내는입니다. 지정 하지 않으면 필드는 null 값을 사용 하 여 추가 됩니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="parameters-collection"></a>Parameters 컬렉션  
 설정 해야 합니다는 [형식](../../../ado/reference/ado-api/type-property-ado.md) 의 속성을 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 를 추가 하기 전에 개체를 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다. 가변 길이 데이터 형식에서 선택 하는 경우 설정 해야 합니다 [크기](../../../ado/reference/ado-api/size-property-ado-parameter.md) 속성을 0 보다 큰 값입니다.  
  
 매개 변수를 직접 설명 공급자에 대 한 호출을 최소화 하 고 저장된 프로시저 또는 매개 변수가 있는 쿼리를 사용 하는 경우 성능이 향상 됩니다. 그러나 매개 변수 속성을 저장된 프로시저를 사용 하 여 연결 하거나 호출 하려는 쿼리 매개 변수가 있는 알아야 합니다.  
  
 사용 합니다 [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 메서드를 **매개 변수** 사용 하 여 확인 하 고 적절 한 속성 설정을 사용 하 여 개체를 **추가** 메서드를 추가할는 [ 매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다. 이 방법으로 설정 하 고 매개 변수 정보에 대 한 공급자를 호출 하지 않고 매개 변수 값을 반환할 수 있습니다. 매개 변수 정보를 제공 하지 않는 공급자를 작성 하는 경우 수동으로를 채우는이 메서드를 사용 해야 합니다 **매개 변수** 전혀 매개 변수를 사용 하려면 컬렉션입니다.  
  
## <a name="fields-collection"></a>Fields 컬렉션  
 *FieldValue* 추가 하는 경우에 매개 변수는 유효한만 **필드** 개체를 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 아닌 개체를 **레코드 집합** 개체. 사용 하 여는 **레코드** 개체 필드를 추가 하 고 동시에 값을 제공할 수 있습니다. 사용 하 여를 **레코드 집합** 개체를 하는 동안 필드를 만들어야 합니다를 **레코드 집합** 닫히지 이며 연 다음 합니다 **레코드 집합** 필드에 값을 할당 하 고.  
  
> [!NOTE]
>  새로운 **필드** 에 추가 된 개체를 **필드** 의 컬렉션을 **레코드** 개체를 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성을 설정 해야 합니다 다른 하기 전에 **필드** 속성을 지정할 수 있습니다. 첫 번째, 특정 값에 대 한는 **값** 속성 할당 받아야 및 [업데이트](../../../ado/reference/ado-api/update-method.md) 에 **필드** 라는 컬렉션입니다. 와 같은 다른 속성에 차례로 [형식](../../../ado/reference/ado-api/type-property-ado.md) 또는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 액세스할 수 있습니다. **필드** 데이터 형식은 개체 (**DataTypeEnum**)에 추가할 수 없습니다는 **필드** 컬렉션 오류가 발생 하면 및: **adArray**, **adChapter**, **adEmpty**하십시오 **adPropVariant**, 및 **adUserDefined**. 데이터 형식은 ADO에서 지원 되지 않습니다는 또한: **adIDispatch**하십시오 **adIUnknown**, 및 **adIVariant**합니다. 이러한 형식에 추가 하는 경우 오류가 발생 하지만 사용 메모리 누수를 비롯 한 예기치 않은 결과 생성할 수 있습니다.  
  
## <a name="recordset"></a>레코드 집합  
 설정 하지 않으면 경우는 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 호출 하기 전에 속성을 **추가** 메서드를 **CursorLocation** 로 설정 됩니다 **adUseClient** ( [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) 값) 때 자동으로 [열기](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 라고 합니다.  
  
 경우 런타임 오류가 발생 합니다 **추가** 메서드를 호출 합니다 **필드** 개방적이 고 컬렉션 **레코드 집합**, 또는 **레코드 집합** 여기서는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성이 설정 되어 있습니다. 필드에만 추가할 수 있습니다는 **레코드 집합** 열려 있지 않으면을 데이터 원본에 아직 연결 되지 않은 합니다. 이 경우 일반적으로 때를 **레코드 집합** 개체가 사용 하 여 만들어집니다는 [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) 메서드 또는 개체 변수에 할당 합니다.  
  
## <a name="record"></a>녹음  
 경우 런타임 오류가 발생 하지 것입니다 합니다 **추가** 메서드를 호출 합니다 **필드** 개방적이 고 컬렉션 **레코드**합니다. 새 필드를 추가할 수는 **필드** 의 컬렉션을 **레코드** 개체입니다. 경우는 **레코드** 에서 파생 된를 **레코드 집합**, 새 필드에 표시 되지 것입니다는 **필드** 의 컬렉션을 **레코드 집합** 개체.  
  
 존재 하지 않는 필드를 작성 및에 추가 합니다 **필드** 컬렉션에 이미 존재 하는 경우에 따라 필드 개체에 값을 할당 하 여 컬렉션입니다. 할당 작업은 자동 생성 및의 추가 트리거한 합니다 **필드** 개체 및 할당을 완료할 수 됩니다.  
  
 추가한 후는 **필드** 에 **필드** 의 컬렉션을 **레코드** 개체를 호출는 **업데이트** 메서드의 **필드**  컬렉션 변경 내용을 저장 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
- [Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [추가 및 CreateParameter 메서드 예제 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [추가 및 CreateParameter 메서드 예제 (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete 메서드 (ADO 필드 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO 매개 변수 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)

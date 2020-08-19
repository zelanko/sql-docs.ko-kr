---
description: Append 메서드(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dd3ee907aa2a7081ca7204dcc1b0b3b069581832
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451265"
---
# <a name="append-method-ado"></a>Append 메서드(ADO)
컬렉션에 개체를 추가 합니다. 컬렉션이 [필드인](../../../ado/reference/ado-api/fields-collection-ado.md)경우 컬렉션에 추가 되기 전에 새 [필드](../../../ado/reference/ado-api/field-object.md) 개체를 만들 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>매개 변수  
 *컬렉션*  
 컬렉션 개체입니다.  
  
 *필드*  
 **Fields** 컬렉션입니다.  
  
 *object*  
 추가할 개체를 나타내는 개체 변수입니다.  
  
 *이름*  
 새 **Field** 개체의 이름을 포함 하는 **문자열** 값으로, *필드*의 다른 개체와 이름이 달라 야 합니다.  
  
 *유형*  
 새 필드의 데이터 형식을 지정 하는 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 값으로, 기본값은 **adEmpty**입니다. 다음 데이터 형식은 ADO에서 지원 되지 않으므로 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)에 새 필드를 추가할 때 사용 하면 안 됩니다. **adIDispatch**, **adIUnknown**, **advariant**.  
  
 *DefinedSize*  
 (선택 사항) 새 필드의 정의 된 크기 (문자 또는 바이트)를 나타내는 **Long** 값입니다. 이 매개 변수의 기본값은 *형식*에서 파생 됩니다. *DefinedSize* 가 255 바이트 보다 큰 필드는 가변 길이 열로 처리 됩니다. *DefinedSize* 의 기본값은 지정 되지 않습니다.  
  
 *특성과*  
 (선택 사항) 새 필드의 특성을 지정 하는 [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) 값으로, 기본값은 **adflddefault**입니다. 이 값을 지정 하지 않으면 필드는 *형식*에서 파생 된 특성을 포함 합니다.  
  
 *FieldValue*  
 (선택 사항) 새 필드의 값을 나타내는 **변형** 입니다. 지정 하지 않으면 필드에 null 값이 추가 됩니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="parameters-collection"></a>Parameters 컬렉션  
 [매개 변수 컬렉션에](../../../ado/reference/ado-api/parameters-collection-ado.md) 추가 하기 전에 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체의 [Type](../../../ado/reference/ado-api/type-property-ado.md) 속성을 설정 해야 합니다. 가변 길이 데이터 형식을 선택 하는 경우에도 [Size](../../../ado/reference/ado-api/size-property-ado-parameter.md) 속성을 0 보다 큰 값으로 설정 해야 합니다.  
  
 매개 변수를 직접 설명 하면 공급자에 대 한 호출이 최소화 되므로 저장 프로시저나 매개 변수가 있는 쿼리를 사용 하는 경우 성능이 향상 됩니다. 그러나 호출 하려는 저장 프로시저 또는 매개 변수가 있는 쿼리와 연결 된 매개 변수의 속성을 알아야 합니다.  
  
 [Createparameter](../../../ado/reference/ado-api/createparameter-method-ado.md) 메서드를 사용 하 여 적절 한 속성 설정이 포함 된 **매개 변수** 개체를 만들고 **Append** 메서드를 사용 하 여 [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션에 추가 합니다. 이렇게 하면 매개 변수 정보에 대 한 공급자를 호출 하지 않고도 매개 변수 값을 설정 하 고 반환할 수 있습니다. 매개 변수 정보를 제공 하지 않는 공급자에 작성 하는 경우 매개 변수를 사용 하기 위해이 메서드를 사용 하 여 **매개 변수** 컬렉션을 수동으로 채워야 합니다.  
  
## <a name="fields-collection"></a>Fields 컬렉션  
 *FieldValue* 매개 변수는 **Recordset** 개체가 아닌 [Record](../../../ado/reference/ado-api/record-object-ado.md) 개체에 **Field** 개체를 추가 하는 경우에만 유효 합니다. **Record** 개체를 사용 하 여 필드를 추가 하 고 동시에 값을 제공할 수 있습니다. **레코드 집합 개체를** 사용 하 여 **레코드 집합** 을 닫는 동안 필드를 만든 다음 **레코드 집합** 을 열고 필드에 값을 할당 합니다.  
  
> [!NOTE]
>  **Record** 개체의 **Fields** 컬렉션에 추가 된 새 **Field** 개체의 경우 다른 **필드** 속성을 지정 하려면 먼저 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성을 설정 해야 합니다. 먼저 **value** 속성의 특정 값이 할당 되 고 라는 **필드** 컬렉션에 대해 [업데이트](../../../ado/reference/ado-api/update-method.md) 되어야 합니다. 그런 다음 [형식](../../../ado/reference/ado-api/type-property-ado.md) 또는 [특성과](../../../ado/reference/ado-api/attributes-property-ado.md) 같은 다른 속성에 액세스할 수 있습니다. 다음 데이터 형식 (**DataTypeEnum**)의 **필드** 개체를 **Fields** 컬렉션에 추가할 수 없으며 **adarray**, **Adarray**, **adEmpty**, **adpropvariant**및 **adarray**와 같은 오류가 발생 합니다. 또한 ADO에서 **adIDispatch**, **adIUnknown**및 **adIVariant**데이터 형식을 지원 하지 않습니다. 이러한 형식에 대해 추가 된 경우 오류가 발생 하지는 않지만 사용 하면 메모리 누수를 포함 하 여 예기치 않은 결과가 발생할 수 있습니다.  
  
## <a name="recordset"></a>레코드 집합  
 **Append** 메서드를 호출 하기 전에 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 설정 하지 않으면 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드가 호출 될 때 **CursorLocation** 가 자동으로 **adUseClient** ( [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) value)로 설정 됩니다.  
  
 열린 **레코드 집합**의 **Fields** 컬렉션이 나 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성이 설정 된 **레코드 집합** 에서 **Append** 메서드를 호출 하면 런타임 오류가 발생 합니다. 열려 있지 않고 데이터 원본에 아직 연결 되지 않은 **레코드 집합** 에만 필드를 추가할 수 있습니다. 이는 일반적으로 [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) 메서드를 사용 하 여 **레코드 집합** 개체를 만들거나 개체 변수에 할당 하는 경우입니다.  
  
## <a name="record"></a>레코드  
 열린 **레코드**의 **Fields** 컬렉션에 대해 **Append** 메서드를 호출 하는 경우에는 런타임 오류가 발생 하지 않습니다. 새 필드가 **Record** 개체의 **Fields** 컬렉션에 추가 됩니다. **레코드** 를 레코드 **집합**에서 파생 한 경우 새 필드는 **레코드 집합** 개체의 **Fields** 컬렉션에 표시 되지 않습니다.  
  
 필드가 이미 컬렉션에 있는 것 처럼 필드 개체에 값을 할당 하 여 존재 하지 않는 필드를 만든 다음 **필드** 컬렉션에 추가할 수 있습니다. 이 할당은 **필드** 개체의 자동 생성 및 추가를 트리거한 다음 할당을 완료 합니다.  
  
 **Record** 개체의 **Fields** 컬렉션에 **필드** 를 추가한 후에는 **fields** 컬렉션의 **Update** 메서드를 호출 하 여 변경 내용을 저장 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
- [Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Parameters 컬렉션(ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Append 및 CreateParameter 메서드 예제 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append 및 CreateParameter 메서드 예제 (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter 메서드 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete 메서드 (ADO Fields Collection)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 메서드 (ADO Parameters Collection)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update 메서드](../../../ado/reference/ado-api/update-method.md)

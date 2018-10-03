---
title: Refresh 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcba9515535e32557470b75267a0e99976a18595
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681627"
---
# <a name="refresh-method-ado"></a>Refresh 메서드(ADO)
공급자를 컬렉션에서 사용할 수 있는 개체를 반영 하도록 및 관련 개체를 업데이트 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Remarks  
 합니다 **새로 고침** 메서드를 호출 하면 컬렉션에 따라 다른 작업을 수행 합니다.  
  
### <a name="parameters"></a>매개 변수  
 사용 하 여는 **새로 고침** 메서드는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 의 컬렉션을 [명령](../../../ado/reference/ado-api/command-object-ado.md) 저장된 프로시저에 대 한 공급자 측 매개 변수 정보를 검색 하는 개체 또는 에 지정 된 매개 변수가 있는 쿼리를 **명령** 개체입니다. 컬렉션은 저장된 프로시저 호출 또는 매개 변수가 있는 쿼리를 지원 하지 않는 공급자에 대 한 비어 있게 됩니다.  
  
 설정 해야 합니다 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성을는 **명령** 유효한 개체 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체를 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성 유효한 명령에 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성을 **adCmdStoredProc** 호출 하기 전에 **새로 고침** 메서드.  
  
 액세스 하는 경우는 **매개 변수** 호출 하기 전에 컬렉션의 **새로 고침** 메서드, ADO 자동으로 메서드를 호출 하 고 사용자에 대 한 컬렉션을 채우는 합니다.  
  
> [!NOTE]
>  사용 하는 경우는 **새로 고침** 공급자에서 매개 변수 정보를 얻는 메서드를 하나 이상의 가변 길이 데이터 형식 반환 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체, ADO 기반 매개 변수에 대 한 메모리를 할당할 수 있습니다 에 허용 된 최대 크기를 실행 하는 동안 오류가 발생할 수 있습니다. 명시적으로 설정 해야 합니다 [크기](../../../ado/reference/ado-api/size-property-ado-parameter.md) 호출 하기 전에 이러한 매개 변수에 대 한 속성을 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 오류를 방지 하는 방법입니다.  
  
### <a name="fields"></a>필드  
 사용 하는 **새로 고침** 메서드는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션이 가시적 효과가 없습니다. 변경 내용을 기본 데이터베이스 구조에서를 검색 하려면 하나를 사용 해야 합니다 [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드 또는 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 책갈피를 지원 하지 않습니다는 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)메서드.  
  
### <a name="properties"></a>속성  
 사용 하는 **새로 고침** 메서드를 **속성** 일부 개체의 컬렉션은 공급자가 노출 하는 동적 속성을 사용 하 여 컬렉션을 채웁니다. 이러한 속성에 기본 제공 속성 ADO 지원 외에도 공급자, 특정 기능에 대 한 정보를 제공합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Axes 컬렉션](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[열 컬렉션](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 컬렉션](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Dimensions 컬렉션](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Errors 컬렉션](../../../ado/reference/ado-api/errors-collection-ado.md)|[필드 컬렉션](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[그룹 컬렉션](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies 컬렉션](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[인덱스 컬렉션](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 컬렉션](../../../ado/reference/adox-api/keys-collection-adox.md)|[Levels 컬렉션](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members 컬렉션](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[매개 변수 컬렉션](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Positions 컬렉션](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Procedures 컬렉션](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[속성 컬렉션](../../../ado/reference/ado-api/properties-collection-ado.md)|[테이블 컬렉션](../../../ado/reference/adox-api/tables-collection-adox.md)|[사용자 컬렉션](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Views 컬렉션](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>관련 항목  
 [Refresh 메서드 예제 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh 메서드 예제 (VC + +)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count 속성 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Refresh 메서드(RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)

---
title: "Refresh 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords: Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e7b776b5d861403909b4856406d30109ad7c6b7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="refresh-method-ado"></a>Refresh 메서드 (ADO)
공급자에 게,에서 사용할 수 있는 개체를 반영 하도록 컬렉션 및 관련 개체를 업데이트 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>주의  
 **새로 고침** 메서드 호출을 컬렉션에 따라 다른 작업을 수행 합니다.  
  
### <a name="parameters"></a>매개 변수  
 사용 하 여는 **새로 고침** 에서 메서드는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 의 컬렉션은 [명령](../../../ado/reference/ado-api/command-object-ado.md) 저장된 프로시저에 대 한 공급자 측 매개 변수 정보를 검색 하는 개체 또는 에 지정 된 매개 변수가 있는 쿼리는 **명령** 개체입니다. 컬렉션은 저장된 프로시저 호출 또는 매개 변수가 있는 쿼리를 지원 하지 않는 공급자에 대 한 비어 있게 됩니다.  
  
 설정 해야는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 의 속성은 **명령** 을 유효한 개체 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성 유효한 명령 및 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성을 **adCmdStoredProc** 호출 하기 전에 **새로 고침** 메서드.  
  
 액세스 하는 경우는 **매개 변수** 호출 하기 전에 컬렉션의 **새로 고침** 메서드, ADO 자동으로 메서드를 호출 하 고 사용자에 대 한 컬렉션을 채웁니다.  
  
> [!NOTE]
>  사용 하는 경우는 **새로 고침** 공급자에서 매개 변수 정보를 얻는 메서드를 하나 이상의 가변 길이 데이터 형식 반환 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체, ADO 따라 매개 변수에 대 한 메모리 할당 에 허용 된 최대 크기를 실행 하는 동안 오류가 발생 합니다. 명시적으로 설정 해야는 [크기](../../../ado/reference/ado-api/size-property-ado-parameter.md) 속성을 호출 하기 전에 이러한 매개 변수는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드 오류를 방지 합니다.  
  
### <a name="fields"></a>필드  
 사용 하 여는 **새로 고침** 에서 메서드는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션이 가시적 효과가 없습니다. 에서 변경 내용을 기본 데이터베이스 구조를 검색 하려면 하나를 사용 해야는 [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드 또는 경우에는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가 책갈피, 지원 하지 않습니다는 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)메서드.  
  
### <a name="properties"></a>속성  
 사용 하는 **새로 고침** 에서 메서드는 **속성** 일부 개체의 컬렉션은 공급자가 노출 하는 동적 속성을 사용 하 여 컬렉션을 채웁니다. 이러한 속성 이외의 기본 제공 속성 ADO에서 지 원하는 공급자에 게 특정 기능에 대 한 정보를 제공합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Axes 컬렉션](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Columns 컬렉션](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 컬렉션](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[차원 컬렉션](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[오류 컬렉션](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields 컬렉션](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[그룹 컬렉션](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies 컬렉션](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[인덱스 컬렉션](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[키 컬렉션입니다.](../../../ado/reference/adox-api/keys-collection-adox.md)|[컬렉션 수준](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members 컬렉션](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters 컬렉션](../../../ado/reference/ado-api/parameters-collection-ado.md)|[위치 컬렉션](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[프로시저 컬렉션](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Properties 컬렉션](../../../ado/reference/ado-api/properties-collection-ado.md)|[테이블 컬렉션](../../../ado/reference/adox-api/tables-collection-adox.md)|[사용자 컬렉션](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[뷰 컬렉션](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>관련 항목:  
 [메서드 예제를 (VB)를 새로 고칩니다.](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [새로 메서드 예제 (VC + +)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count 속성 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Refresh 메서드(RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)

---
description: Refresh 메서드(ADO)
title: Refresh 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 66324860f931a919cccc36d3de9464d2ad2e48d0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989614"
---
# <a name="refresh-method-ado"></a>Refresh 메서드(ADO)
공급자와 관련 하 여 사용 가능한 개체를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>설명  
 **Refresh** 메서드는 호출 하는 컬렉션에 따라 다른 작업을 수행 합니다.  
  
### <a name="parameters"></a>매개 변수  
 [Command](./command-object-ado.md) 개체의 [Parameters](./parameters-collection-ado.md) 컬렉션에 **Refresh** 메서드를 사용 하 여 **명령** 개체에 지정 된 저장 프로시저 또는 매개 변수가 있는 쿼리에 대 한 공급자 측 매개 변수 정보를 검색 합니다. 저장 프로시저 호출 또는 매개 변수가 있는 쿼리를 지원 하지 않는 공급자에 대해서는 컬렉션이 비어 있게 됩니다.  
  
 **Refresh** 메서드를 호출 하기 전에 **명령** 개체의 [ActiveConnection](./activeconnection-property-ado.md) 속성을 유효한 [연결](./connection-object-ado.md) 개체, [CommandText](./commandtext-property-ado.md) 속성을 유효한 명령으로, [CommandType](./commandtype-property-ado.md) 속성을 **adCmdStoredProc** 로 설정 해야 합니다.  
  
 **Refresh** 메서드를 호출 하기 전에 **매개 변수** 컬렉션에 액세스 하는 경우 ADO에서 자동으로 메서드를 호출 하 고 컬렉션을 채웁니다.  
  
> [!NOTE]
>  **Refresh** 메서드를 사용 하 여 공급자에서 매개 변수 정보를 가져오고 하나 이상의 가변 길이 데이터 형식 [매개 변수](./parameter-object.md) 개체를 반환 하는 경우, ADO는 실행 중에 오류가 발생 하는 최대 크기를 기준으로 매개 변수에 대 한 메모리를 할당할 수 있습니다. 오류를 방지 하기 위해 [Execute](./execute-method-ado-command.md) 메서드를 호출 하기 전에 이러한 매개 변수의 [Size](./size-property-ado-parameter.md) 속성을 명시적으로 설정 해야 합니다.  
  
### <a name="fields"></a>필드  
 [Fields](./fields-collection-ado.md) 컬렉션에 **Refresh** 메서드를 사용 해도 아무런 효과가 없습니다. 기본 데이터베이스 구조에서 변경 내용을 검색 하려면 [Requery](./requery-method.md) 메서드를 사용 하거나 [레코드 집합](./recordset-object-ado.md) 개체가 책갈피를 지원 하지 않는 경우 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드를 사용 해야 합니다.  
  
### <a name="properties"></a>속성  
 일부 개체의 **Properties** 컬렉션에 **Refresh** 메서드를 사용 하면 공급자가 노출 하는 동적 속성을 사용 하 여 컬렉션을 채웁니다. 이러한 속성은 ADO에서 지 원하는 기본 제공 속성 외에 공급자와 관련 된 기능에 대 한 정보를 제공 합니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [축 컬렉션](../ado-md-api/axes-collection-ado-md.md)  
        [Columns 컬렉션](../adox-api/columns-collection-adox.md)  
        [CubeDefs 컬렉션](../ado-md-api/cubedefs-collection-ado-md.md)  
        [차원 컬렉션](../ado-md-api/dimensions-collection-ado-md.md)  
        [Errors 컬렉션](./errors-collection-ado.md)  
        [Fields 컬렉션](./fields-collection-ado.md)  
        [Groups 컬렉션](../adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [계층 컬렉션](../ado-md-api/hierarchies-collection-ado-md.md)  
        [Indexes 컬렉션](../adox-api/indexes-collection-adox.md)  
        [Keys 컬렉션](../adox-api/keys-collection-adox.md)  
        [수준 컬렉션](../ado-md-api/levels-collection-ado-md.md)  
        [Members 컬렉션](../ado-md-api/members-collection-ado-md.md)  
        [Parameters 컬렉션](./parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [위치 컬렉션](../ado-md-api/positions-collection-ado-md.md)  
        [프로시저 컬렉션](../adox-api/procedures-collection-adox.md)  
        [속성 컬렉션](./properties-collection-ado.md)  
        [Tables 컬렉션](../adox-api/tables-collection-adox.md)  
        [사용자 컬렉션](../adox-api/users-collection-adox.md)  
        [Views 컬렉션](../adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Refresh 메서드 예제 (VB)](./refresh-method-example-vb.md)   
 [Refresh 메서드 예제 (VC + +)](./refresh-method-example-vc.md)   
 [Count 속성 (ADO)](./count-property-ado.md)   
 [Refresh 메서드(RDS)](../rds-api/refresh-method-rds.md)
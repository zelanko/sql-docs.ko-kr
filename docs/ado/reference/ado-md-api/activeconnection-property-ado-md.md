---
title: ActiveConnection 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
author: rothja
ms.author: jroth
ms.openlocfilehash: 13a24320f7b49d8d2a0e1341bff2d9a4cca575dd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765324"
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection 속성(ADO MD)
현재 셀 집합 또는 카탈로그가 현재 속해 있는 ADO [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **연결 또는 연결 개체를** 정의 하는 문자열을 포함 하는 **Variant** 를 설정 하거나 반환 합니다. 기본값은 비어 있습니다.  
  
## <a name="remarks"></a>설명  
 이 속성을 유효한 ADO **연결** 개체 또는 유효한 연결 문자열로 설정할 수 있습니다. 이 속성을 연결 문자열로 설정 하면 공급자는이 정의를 사용 하 여 새 **연결** 개체를 만들고 연결을 엽니다.  
  
 [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) 메서드의 *ActiveConnection* 인수를 사용 하 여 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체를 열면 **ActiveConnection** 속성이 인수 값을 상속 합니다.  
  
 [카탈로그](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) 개체의 **ActiveConnection** 속성을 **Nothing** 으로 설정 하면 [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) 컬렉션의 데이터, 관련 된 [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md)및 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체를 비롯 한 연결 된 데이터가 해제 됩니다. **카탈로그** 를 여는 데 사용 된 **연결** 개체를 닫는 것은 **ActiveConnection** 속성을 **Nothing**으로 설정 하는 것과 동일한 효과를 가집니다.  
  
 **카탈로그** 개체의 **ActiveConnection** 속성에서 참조 하는 연결의 기본 데이터베이스를 변경 하면 **카탈로그**의 내용이 무효화 됩니다.  
  
 열린 **셀 집합** 개체의 **ActiveConnection** 속성을 변경 하려고 하면 오류가 발생 합니다.  
  
> [!NOTE]
>  Visual Basic에서 **ActiveConnection** 속성을 **Connection** 개체로 설정할 때 **Set** 키워드를 사용 해야 합니다. **Set** 키워드를 생략 하는 경우 실제로 **ActiveConnection** 속성은 **연결** 개체의 기본 속성인 **ConnectionString**과 동일 하 게 설정 됩니다. 코드가 작동 합니다. 그러나 성능에 부정적인 영향을 미칠 수 있는 데이터 원본에 대 한 추가 연결을 만듭니다.  
  
 MSOLAP 데이터 공급자를 사용 하는 경우 연결 문자열의 데이터 원본을 서버 이름으로 설정 하 고 초기 카탈로그를 데이터 원본의 카탈로그 이름으로 설정 합니다. 서버에서 연결이 끊어진 큐브 파일에 연결 하려면 위치를에 대 한 전체 경로로 설정 합니다. .CUB 파일. 두 경우 모두 공급자 이름으로 공급자를 설정 합니다. 예를 들어 다음 문자열은 MSOLAP 공급자를 사용 하 여 **Servername**이라는 서버의 Bobs Video Store 라는 카탈로그에 연결 합니다.  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 다음 문자열은 C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub 위치에서 로컬 큐브 파일에 연결 합니다.  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Catalog 개체(ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>참고 항목  
 [셀 집합 예제 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open 메서드(ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)

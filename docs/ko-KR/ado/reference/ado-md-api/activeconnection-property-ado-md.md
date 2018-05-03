---
title: ADO MD ActiveConnection 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 708f33d5cf4881040bef714ce62d9082ecc6528f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="activeconnection-property-ado-md"></a>ADO MD ActiveConnection 속성
어떤 ado 나타냅니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 카탈로그 현재 속한 또는 현재 셀 집합 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **Variant** 연결을 정의 하는 문자열을 포함 하는 또는 **연결** 개체입니다. 기본값은 비어 있습니다.  
  
## <a name="remarks"></a>주의  
 유효한 ADO에이 속성을 설정할 수 **연결** 개체 또는 유효한 연결 문자열입니다. 이 속성은 연결 문자열을 설정 하면 공급자 만들며 새 **연결** 이 정의 사용 하 여 연결을 엽니다.  
  
 사용 하는 경우는 *ActiveConnection* 의 인수는 [열고](../../../ado/reference/ado-md-api/open-method-ado-md.md) 여 메서드를 한 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체는 **ActiveConnection** 속성은 인수의 값을 상속 합니다.  
  
 설정의 **ActiveConnection** 속성은 [카탈로그](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) 개체를 **Nothing** 의 데이터를 포함 하 여 관련된 데이터를 해제는 [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) 컬렉션과 관련 된 모든 [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md), 및 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체입니다. 닫기는 **연결** 하는 데 사용 된 개체는 **카탈로그** 같은 결과가 설정으로는 **ActiveConnection** 속성을 **Nothing**.  
  
 참조 하는 연결의 기본 데이터베이스를 변경는 **ActiveConnection** 속성은 **카탈로그** 내용의 압축을 무효화 하는 개체는 **카탈로그**합니다.  
  
 변경 하려고 하면 오류가 발생 합니다는 **ActiveConnection** 열린에 대 한 속성 **셀 집합** 개체입니다.  
  
> [!NOTE]
>  Visual Basic에서 사용 해야는 **설정** 설정할 때 키워드는 **ActiveConnection** 속성을 한 **연결** 개체입니다. 생략 하면는 **설정** 키워드를 실제로 설정 된 **ActiveConnection** 속성에는 **연결** 개체의 기본 속성  **ConnectionString**합니다. 코드가 작동 합니다. 그러나 성능에 부정적인 영향을 줄 수 있는 데이터 원본에 대 한 추가 연결에 만들어집니다.  
  
 MSOLAP 데이터 공급자를 사용할 때는 서버 이름에 연결 문자열에 데이터 소스를 설정 하 고 데이터 원본의 초기 카탈로그는 카탈로그의 이름으로 설정 합니다. 서버에서 연결이 끊어진 큐브 파일에 연결할 위치 설정의 전체 경로를 합니다. 주로 큐브 파일입니다. 두 경우 모두 공급자 이름으로 공급자를 설정 합니다. 다음 문자열 이라는 서버의 Bobs 비디오 저장소 라는 카탈로그를 연결할 때 MSOLAP 공급자를 사용 하는 예를 들어 **Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 다음 문자열 C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub 위치에서 로컬 큐브 파일에 연결 됩니다.  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Catalog 개체(ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [셀 집합 예제 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open 메서드(ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)

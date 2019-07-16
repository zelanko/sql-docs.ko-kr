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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae0b32385b98ac1b48688a7f89bbd7c91842a106
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911590"
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection 속성(ADO MD)
에 ADO [연결](../../../ado/reference/ado-api/connection-object-ado.md) 카탈로그 현재 속한 또는 현재 셀 집합 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **Variant** 연결을 정의 하는 문자열을 포함 하는 또는 **연결** 개체입니다. 기본적으로 비어 있습니다.  
  
## <a name="remarks"></a>설명  
 유효한 ADO에이 속성을 설정할 수 있습니다 **연결** 개체 또는 유효한 연결 문자열입니다. 이 속성을 설정 하 여 연결 문자열에 공급자를 만듭니다 **연결** 이 정의 사용 하 여 연결을 엽니다.  
  
 사용 하는 경우는 *ActiveConnection* 인수를 [엽니다](../../../ado/reference/ado-md-api/open-method-ado-md.md) 를 여는 메서드를 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체를 **ActiveConnection** 속성은 인수의 값을 상속 합니다.  
  
 설정 합니다 **ActiveConnection** 의 속성을 [카탈로그](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) 개체를 **Nothing** 에서 데이터를 포함 하 여 연결 된 데이터를 해제를 [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) 컬렉션과 관련 된 모든 [차원](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)를 [계층](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)를 [수준](../../../ado/reference/ado-md-api/level-object-ado-md.md), 및 [멤버](../../../ado/reference/ado-md-api/member-object-ado-md.md) 개체입니다. 닫기는 **연결** 열려는 사용 된 개체를 **카탈로그** 설정으로 동일한 효과가 **ActiveConnection** 속성을 **Nothing**.  
  
 참조 하는 연결의 기본 데이터베이스를 변경 합니다 **ActiveConnection** 의 속성을 **카탈로그** 개체의 내용을 무효화를 **카탈로그**.  
  
 변경 하려고 하면 오류가 발생 합니다 **ActiveConnection** 개방적이 고 속성 **셀 집합** 개체입니다.  
  
> [!NOTE]
>  Visual basic에서는를 사용 해야 합니다 **설정** 설정 하는 경우 키워드는 **ActiveConnection** 속성을를 **연결** 개체. 생략 하면는 **설정** 키워드를 실제로 설정 된 **ActiveConnection** 속성이 **연결** 개체의 기본 속성  **ConnectionString**합니다. 코드는 작동 합니다. 그러나 성능이 저하 될 수 있습니다 하는 데이터 원본에 대 한 추가 연결에 만들어집니다.  
  
 MSOLAP 데이터 공급자를 사용 하면 데이터 원본 연결 문자열에 서버 이름 설정 하 고 데이터 원본에서 카탈로그의 이름으로 초기 카탈로그를 설정 합니다. 서버에서 연결이 끊어진 큐브 파일에 연결 하려면 전체 경로 위치를 설정 합니다. 큐브 파일입니다. 두 경우 모두 공급자 이름으로 공급자를 설정 합니다. 다음 문자열 이라는 서버의 Bobs 비디오 저장소 라는 카탈로그를 연결할 때 MSOLAP 공급자를 사용 하는 예를 들어 **Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 다음 문자열 C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub 위치의 로컬 큐브 파일에 연결합니다.  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Catalog 개체(ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Cellset 예제 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open 메서드(ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)

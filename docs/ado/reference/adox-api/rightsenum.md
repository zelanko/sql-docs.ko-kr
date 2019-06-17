---
title: RightsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a34cbd8ee3d274d3b3d45049611ca9cc99fa7758
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718841"
---
# <a name="rightsenum"></a>RightsEnum
개체에 권한 또는 그룹 또는 사용자에 대 한 권한을 지정합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (및 H4000)|사용자 또는 그룹에이 형식의 새 개체를 만들 수 있는 권한이 있습니다.|  
|**adRightDelete**|65536 (및 H10000)|사용자 또는 그룹 개체에서 데이터를 삭제할 권한이 있습니다. 와 같은 개체에 대 한 **테이블**, 레코드의 데이터 값을 삭제 하는 사용자가 있습니다.|  
|**adRightDrop**|256 (및 H100)|사용자나 그룹이 카탈로그에서 개체를 제거할 권한이 있습니다. 예를 들어 **테이블** DROP TABLE SQL 명령으로 삭제할 수 있습니다.|  
|**adRightExclusive**|512 (및 H200)|사용자 또는 그룹에 개체를 단독으로 액세스할 수 있는 권한이 있습니다.|  
|**adRightExecute**|536870912 (&H20000000)|사용자 또는 그룹 개체를 실행할 권한이 있습니다.|  
|**adRightFull**|268435456 (및 H10000000)|사용자 또는 그룹에 모든 개체입니다.|  
|**adRightInsert**|32768 (및 H8000)|사용자 또는 그룹에 개체를 삽입할 수 있는 권한이 있습니다. 와 같은 개체에 대 한 **테이블**는 사용자가 테이블에 데이터를 삽입 합니다.|  
|**adRightMaximumAllowed**|33554432 (&AMP; H 2000000)|사용자 또는 그룹에 최대 개수의 공급자가 허용 되는 권한 합니다. 특정 사용 권한은 공급자에 따라 다릅니다.|  
|**adRightNone**|0|사용자 또는 그룹에 개체에 대 한 권한이 없습니다.|  
|**adRightRead**|-2147483648 (&H80000000)|사용자 또는 그룹에 개체를 읽을 수 있는 권한이 있습니다. 와 같은 개체에 대 한 [테이블](../../../ado/reference/adox-api/table-object-adox.md), 사용자가 테이블의 데이터를 읽을 수 있습니다.|  
|**adRightReadDesign**|1024 (&AMP; H400)|사용자 또는 그룹에 개체에 대 한 디자인을 읽을 수 있는 권한이 있습니다.|  
|**adRightReadPermissions**|131072 (및 H20000)|사용자 또는 그룹 수를 보려면 변경 하지는 않고 카탈로그에 있는 개체에 대 한 특정 권한.|  
|**adRightReference**|8192 (&AMP; H2000)|사용자 또는 그룹에 개체를 참조할 수 있는 권한이 있습니다.|  
|**adRightUpdate**|1073741824 (및 H40000000)|사용자 또는 그룹에 개체를 업데이트할 수 있는 권한이 있습니다. 와 같은 개체에 대 한 **테이블**, 사용자가 테이블의 데이터를 업데이트할 수 있습니다.|  
|**adRightWithGrant**|4096 (&H1000)|사용자 또는 그룹 개체에 사용 권한을 부여할 권한이 있습니다.|  
|**adRightWriteDesign**|2048 (&AMP; H800)|사용자 또는 그룹에 개체에 대 한 디자인을 수정할 수 있는 권한이 있습니다.|  
|**adRightWriteOwner**|524288 (&H80000)|사용자 또는 그룹에 개체의 소유자를 수정할 수 있는 권한이 있습니다.|  
|**adRightWritePermissions**|262144 (및 H40000)|사용자 또는 그룹을 카탈로그에 있는 개체에 대 한 특정 권한을 수정할 수 있습니다.|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[GetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[SetPermissions 메서드(ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|

---
title: StartMode 속성 (SqlService 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- StartMode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c3bed01976385885d84768101d8b64c9436fdcea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307493"
---
# <a name="startmode-property-sqlservice-class"></a>StartMode 속성(SqlService 클래스)
  서비스의 시작 모드를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.StartMode [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서비스의 모드를 지정하는 uint32 값입니다.  
  
 다음 값 중 하나일 수 있습니다.  
  
 부팅  
 값 = 0. 운영 체제 로더에 의해 서비스가 시작됩니다. 이 옵션은 드라이버 서비스에 대해서만 유효합니다.  
  
 시스템  
 값 = 1입니다. `IoInitSystem` 메서드에 의해 서비스가 시작됩니다. 이 옵션은 드라이버 서비스에 대해서만 유효합니다.  
  
 자동  
 값 = 2입니다. 시스템 시작 중 서비스 제어 관리자에 의해 자동으로 서비스가 시작됩니다.  
  
 수동  
 값 = 3입니다. 프로세스에서 `StartService` 메서드를 호출할 때 컴퓨터 관리자에 의해 서비스가 시작됩니다.  
  
 사용 안 함  
 값 = 4입니다. 서비스를 시작할 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서비스 시작 및 중지](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

---
description: StartMode 속성(SqlService 클래스)
title: StartMode 속성 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartMode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 608214cf9d4eca2601c0f8bee7b82570ec936ea6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418759"
---
# <a name="startmode-property-sqlservice-class"></a>StartMode 속성(SqlService 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서비스의 시작 모드를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서비스의 모드를 지정하는 uint32 값입니다.  
  
 다음 값 중 하나일 수 있습니다.  
  
 부팅  
 값 = 0. 운영 체제 로더에 의해 서비스가 시작됩니다. 이 옵션은 드라이버 서비스에 대해서만 유효합니다.  
  
 시스템  
 값 = 1입니다. **Ioinitsystem** 메서드에 의해 서비스가 시작 되었습니다. 이 옵션은 드라이버 서비스에 대해서만 유효합니다.  
  
 자동  
 값 = 2입니다. 시스템 시작 중 서비스 제어 관리자에 의해 자동으로 서비스가 시작됩니다.  
  
 설명서  
 값 = 3입니다. 프로세스에서 **StartService** 메서드를 호출할 때 컴퓨터 관리자에 의해 서비스가 시작 됩니다.  
  
 사용 안 함  
 값 = 4입니다. 서비스를 시작할 수 없습니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

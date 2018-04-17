---
title: SetDefaults 메서드 (ClientSettings 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SetDefaults Method (ClientSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72cf889c04c8c3bd8ca60ad7e4c5af417c8ce95d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="clientsettings-class---setdefaults-method"></a>ClientSettings 클래스-SetDefaults 메서드
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  인스턴스에 대 한 모든 기본값을 설정는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기존 데이터 덮어쓰기 옵션을 사용 하 여 클라이언트입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 A **ClientSettings** 을 나타내는 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 인스턴스.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*OverwriteAll*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 인스턴스의 기존 값을 덮어쓸지 여부를 지정하는 부울 값입니다. **true** 인 경우 기존 데이터를 덮어쓰고 **false** 인 경우 기존 데이터를 덮어쓰지 않습니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>주의  
  

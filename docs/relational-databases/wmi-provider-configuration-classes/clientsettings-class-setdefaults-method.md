---
description: ClientSettings 클래스 - SetDefaults 메서드
title: SetDefaults 메서드 (ClientSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ClientSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3570423483ea398be21a41e3b26d7d1c3d61c064
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540130"
---
# <a name="clientsettings-class---setdefaults-method"></a>ClientSettings 클래스 - SetDefaults 메서드
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기존 데이터를 덮어쓰는 옵션을 사용 하 여 클라이언트 인스턴스에 대 한 모든 기본값을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 **ClientSettings** 클라이언트 인스턴스를 나타내는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*OverwriteAll*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 인스턴스의 기존 값을 덮어쓸지 여부를 지정하는 부울 값입니다. **true** 인 경우 기존 데이터를 덮어쓰고 **false** 인 경우 기존 데이터를 덮어쓰지 않습니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  

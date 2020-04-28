---
title: SetDefaults 메서드 (ServerSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 76e4cfab-4b15-4da4-bb2f-8aac6f927f79
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86e15376bd56a439e0763e79a5c166d7023125ea
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73660268"
---
# <a name="setdefaults-method-serversettings-class"></a>SetDefaults 메서드(ServerSettings 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  기존 데이터를 덮어쓰는 옵션을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용 하 여 인스턴스에 대 한 모든 기본값을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 클라이언트 인스턴스를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 나타내는 [serversettings 클래스](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*OverwriteAll*|인스턴스의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]기존 값을 덮어쓸지 여부를 지정 하는 부울 값입니다. 기존 데이터를 덮어쓰려면 **true** 이 고, 기존 데이터를 덮어쓰지 않을 경우 **false** 입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 U**int32** 값으로, 0은 서비스가 수정 되었음을 나타내고 1은 요청이 지원 되지 않음을 나타내며 다른 모든 숫자는 오류를 표시 합니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

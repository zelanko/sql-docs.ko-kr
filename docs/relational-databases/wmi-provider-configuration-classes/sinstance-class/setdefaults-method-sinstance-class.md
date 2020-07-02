---
title: SetDefaults 메서드 (SInstance)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: dc3c6a85-0711-4688-bf4f-91168c57af28
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b29cf5b1f0b10965c0545c91b84d13a8caea361c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731409"
---
# <a name="setdefaults-method-sinstance-class"></a>SetDefaults 메서드(SInstance 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)]기존 데이터를 덮어쓰는 옵션을 사용 하 여 인스턴스에 대 한 모든 기본값을 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서버 인스턴스를 나타내는 [Sinstance 클래스](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*OverwriteAll*|클라이언트 인스턴스의 기존 값을 덮어쓸지 여부를 지정 하는 부울 값입니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . 기존 데이터를 덮어쓴 경우 **true** 이 고, 기존 데이터를 덮어쓰지 않는 경우 **false** 입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

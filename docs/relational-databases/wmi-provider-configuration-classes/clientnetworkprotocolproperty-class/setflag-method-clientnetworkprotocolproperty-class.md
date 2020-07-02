---
title: SetFlag 메서드 (ClientNetworkProtocolProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetFlag Method (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetFlag method
ms.assetid: 0407520f-2f84-4f68-b2b7-429697286c1b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 609bfb541789bc0a11bf0d9a56f417a65008f361
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759936"
---
# <a name="setflag-method-clientnetworkprotocolproperty-class"></a>SetFlag 메서드(ClientNetworkProtocolProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  [Propertyidx 속성 (ClientNetworkProtocolProperty 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) 값에서 참조 하는 현재 속성의 플래그를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetFlag(BoolValue) [=]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 클라이언트에서 사용 하는 네트워크 프로토콜의 특성을 나타내는 [Clientnetworkprotocolproperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*BoolValue*|플래그의 새 값을 지정하는 부울 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  

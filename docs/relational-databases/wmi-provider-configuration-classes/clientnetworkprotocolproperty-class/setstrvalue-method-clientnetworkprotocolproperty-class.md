---
title: SetStrValue 메서드 (ClientNetworkProtocolProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStrValue Method (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStrValue method
ms.assetid: 4ff80124-6e2e-4d96-a692-57c17b53c55e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1a08c38a074c573bbeda77180399dca1f0267ae1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759907"
---
# <a name="setstrvalue-method-clientnetworkprotocolproperty-class"></a>SetStrValue 메서드(ClientNetworkProtocolProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  [PropertyIdx 속성(ClientNetworkProtocolProperty 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) 값에서 참조하는 현재 속성의 문자열 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetStrValue(StrValue)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [클라이언트에서 사용하는 네트워크 프로토콜의 특성을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) ClientNetworkProtocolProperty 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*StrValue*|현재 속성의 새 값을 지정하는 문자열 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 uint32 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  

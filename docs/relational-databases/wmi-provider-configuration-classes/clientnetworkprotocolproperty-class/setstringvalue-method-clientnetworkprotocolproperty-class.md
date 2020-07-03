---
title: SetStringValue 메서드 (ClientNetworkProtocolProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStringValue Method (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStringValue method
ms.assetid: 88d67b22-0eea-48c9-ab73-e0b4907953df
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 60392a04607e2bc2c5c4b06edd940409d58af1a8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881028"
---
# <a name="setstringvalue-method-clientnetworkprotocolproperty-class"></a>SetStringValue 메서드(ClientNetworkProtocolProperty 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [PropertyIdx 속성(ClientNetworkProtocolProperty 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) 값에서 참조하는 현재 속성의 문자열 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetStringValue(StrValue)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 클라이언트에서 사용 하는 네트워크 프로토콜의 특성을 나타내는 [Clientnetworkprotocolproperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*StrValue*|현재 속성의 새 값을 지정하는 문자열 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  

---
title: PropertyIdx 속성 (ClientNetworkProtocolProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyIdx Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e5a8dcb5357a758a129a1a9dda654ccaeb6de4a3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85638855"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx 속성(ClientNetworkProtocolProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  [Clientnetworkprotocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 개체의 [Properties 속성 (clientnetworkprotocol 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/properties-property-clientnetworkprotocol-class.md) 에서 참조 하는 속성 배열에서 속성의 인덱스 값을 가져오거나 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 클라이언트에서 사용 하는 네트워크 프로토콜의 특성을 나타내는 [Clientnetworkprotocolproperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 현재 속성의 배열 인덱스 값을 지정 하는 **uint32** 값입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  

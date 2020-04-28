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
ms.openlocfilehash: b3330ab2be25fdeccab3c39d6d9528adedaabc0e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73660368"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx 속성(ClientNetworkProtocolProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [Clientnetworkprotocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 개체의 [Properties 속성 (clientnetworkprotocol 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/properties-property-clientnetworkprotocol-class.md) 에서 참조 하는 속성 배열에서 속성의 인덱스 값을 가져오거나 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 사용 하는 네트워크 프로토콜의 특성을 나타내는 [clientnetworkprotocolproperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 현재 속성의 배열 인덱스 값을 지정 하는 **uint32** 값입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  

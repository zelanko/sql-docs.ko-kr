---
title: SetFlag 메서드 (ClientNetworkProtocolProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetFlag Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetFlag method
ms.assetid: 0407520f-2f84-4f68-b2b7-429697286c1b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6c33eca0bf3281243aeee42ed89001cf9108d5d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245087"
---
# <a name="setflag-method-clientnetworkprotocolproperty-class"></a>SetFlag 메서드(ClientNetworkProtocolProperty 클래스)
  [Propertyidx 속성 (ClientNetworkProtocolProperty 클래스)](clientnetworkprotocolproperty-class.md) 값에서 참조 하는 현재 속성의 플래그를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetFlag(  
BoolValue  
) [=]  
```  
  
## <a name="parts"></a>부분  
 *개체가*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 사용 하는 네트워크 프로토콜의 특성을 나타내는 [clientnetworkprotocolproperty 클래스](clientnetworkprotocolproperty-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*BoolValue*|플래그의 새 값을 지정하는 부울 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 
  `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  

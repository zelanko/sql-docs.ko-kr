---
title: "SetStrValue 메서드 (ClientNetworkProtocolProperty 클래스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SetStrValue Method (ClientNetworkProtocolProperty Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetStrValue method
ms.assetid: 4ff80124-6e2e-4d96-a692-57c17b53c55e
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1596ed5660a0d7a8d469dfc93b66c11222a9c589
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="setstrvalue-method-clientnetworkprotocolproperty-class"></a>SetStrValue 메서드(ClientNetworkProtocolProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]참조 하는 현재 속성의 문자열 값을 설정 하는 [PropertyIdx 속성 (ClientNetworkProtocolProperty 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetStrValue(StrValue)  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 [클라이언트에서 사용하는 네트워크 프로토콜의 특성을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) ClientNetworkProtocolProperty 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*StrValue*|현재 속성의 새 값을 지정하는 문자열 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 uint32 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  

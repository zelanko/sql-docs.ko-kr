---
title: NumberOfFlags 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- NumberOfFlags Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: 7a656644-2154-419f-9787-99877f597770
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ced27995713e0863bc95ab24145fef745b52b20f
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51216411"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>NumberOfFlags 속성(ClientNetworkProtocol 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  지정한 클라이언트 네트워크 프로토콜에 필요한 플래그 옵션의 수를 가져옵니다 합니다 [SetOrderValue 메서드 (ClientNetworkProtocol 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [클라이언트에서 사용하는 네트워크 프로토콜을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 A **Uint32** 값에서 참조 하는 클라이언트 네트워크 프로토콜에 필요한 플래그 옵션의 수를 지정 하는 **OrderValue** 속성입니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  

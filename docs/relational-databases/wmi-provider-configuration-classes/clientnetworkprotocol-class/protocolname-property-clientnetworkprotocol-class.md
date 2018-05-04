---
title: ProtocolName 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ProtocolName Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolName property
ms.assetid: f8527121-fbcd-4d30-9b4a-1461149cb5a8
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6f6b45ca97f6cd9361f6725fe0bdefcfc7be4385
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="protocolname-property-clientnetworkprotocol-class"></a>ProtocolName 속성(ClientNetworkProtocol 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  지정한 현재 네트워크 프로토콜의 이름을 가져옵니다는 [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 A [ClientNetworkProtocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 에서 사용 하는 네트워크 프로토콜을 나타내는 개체는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 현재 클라이언트의 이름을 지정 하는 문자열 값에서 참조 네트워크 프로토콜의 [SetOrderValue 메서드 (ClientNetworkProtocol 클래스)](http://technet.microsoft.com/library/ms179295.aspx)합니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  

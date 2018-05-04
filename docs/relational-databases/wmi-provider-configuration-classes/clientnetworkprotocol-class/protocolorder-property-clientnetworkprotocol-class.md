---
title: ProtocolOrder 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ProtocolOrder Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 961aad44364a5fca62afff1a00c7aef34be482b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 속성(ClientNetworkProtocol 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  네트워크 프로토콜에 지정 된 대로 현재 참조 되는 클라이언트의 순서 번호를 가져옵니다는 [SetOrderValue 메서드 (ClientNetworkProtocol 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 A [ClientNetworkProtocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 에서 사용 하는 네트워크 프로토콜을 나타내는 개체는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 A **uint32** 가 설정한 현재 참조 되는 클라이언트 네트워크 프로토콜의 순서 번호를 지정 하는 값은 **OrderValue** 메서드. 클라이언트 네트워크 프로토콜이 해제된 경우 이 값은 0입니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)   
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  

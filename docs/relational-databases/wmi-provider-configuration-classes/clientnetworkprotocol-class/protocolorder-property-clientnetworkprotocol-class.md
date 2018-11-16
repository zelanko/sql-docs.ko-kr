---
title: ProtocolOrder 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolOrder Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5f0112546c356c8523392a63c4dcefa65769861a
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51669742"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 속성(ClientNetworkProtocol 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  현재 참조 되는 클라이언트의 순서 번호를 지정 된 대로 네트워크 프로토콜을 가져옵니다 합니다 [SetOrderValue 메서드 (ClientNetworkProtocol 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [ClientNetworkProtocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 사용 되는 네트워크 프로토콜을 나타내는 개체를 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 A **uint32** 에서 설정한 대로 현재 참조 되는 클라이언트 네트워크 프로토콜의 순서 번호를 지정 하는 값을 **OrderValue** 메서드. 클라이언트 네트워크 프로토콜이 해제된 경우 이 값은 0입니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 프로토콜 구성](https://technet.microsoft.com/library/ms181035.aspx)   
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://technet.microsoft.com/library/ms181035.aspx)  
  
  

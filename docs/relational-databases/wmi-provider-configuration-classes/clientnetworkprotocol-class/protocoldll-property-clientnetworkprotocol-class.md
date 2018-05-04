---
title: ProtocolDLL 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
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
- ProtocolDLL Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: fe8650d5-7b9d-46f8-bf74-baf1d9d2a06a
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 895086e2164f6766cc6c83d63521c95c062321c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>ProtocolDLL 속성(ClientNetworkProtocol 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  지정한 네트워크 프로토콜에 필요한.dll 파일의 이름을 가져옵니다는 [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 A [ClientNetworkProtocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 에서 사용 하는 네트워크 프로토콜을 나타내는 개체는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 클라이언트 네트워크 프로토콜에 필요한 프로토콜 .dll 파일을 지정하는 문자열 값입니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  

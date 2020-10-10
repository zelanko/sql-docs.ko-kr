---
description: ProtocolDLL 속성(ClientNetworkProtocol 클래스)
title: ProtocolDLL 속성 (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolDLL Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: fe8650d5-7b9d-46f8-bf74-baf1d9d2a06a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 54d992dd3d9b3604644f985f9e7db5f523b553f9
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889037"
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>ProtocolDLL 속성(ClientNetworkProtocol 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)에서 지정한 네트워크 프로토콜에 필요한 .dll 파일의 이름을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 클라이언트에서 사용 하는 네트워크 프로토콜을 나타내는 [Clientnetworkprotocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 클라이언트 네트워크 프로토콜에 필요한 프로토콜 .dll 파일을 지정하는 문자열 값입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  

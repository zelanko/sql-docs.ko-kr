---
description: IpAddresses 속성(ServerNetworkProtocol 클래스)
title: IpAddresses 속성 (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- IpAddresses Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- IpAddresses property
ms.assetid: e5d66f7e-9719-436e-b723-12d56f914a05
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9bd31cf4758415cc235942607319a26c1a283437
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545461"
---
# <a name="ipaddresses-property-servernetworkprotocol-class"></a>IpAddresses 속성(ServerNetworkProtocol 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서버 네트워크 프로토콜과 연결된 IP 주소를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.IpAddresses [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 인스턴스에서 사용 하는 네트워크 프로토콜을 나타내는 **Servernetworkprotocol** 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서버 네트워크 프로토콜에서 지 원하는 IP 주소를 나타내는 [ServerNetworkProtocolIPAdress 클래스](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) 개체의 배열입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

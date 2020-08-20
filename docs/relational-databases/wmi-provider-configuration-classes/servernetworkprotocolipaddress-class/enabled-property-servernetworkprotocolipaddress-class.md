---
description: Enabled 속성(ServerNetworkProtocolIpAddress 클래스)
title: Enabled 속성 (ServerNetworkProtocolIpAddress)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Enabled Property (ServerNetworkProtocolIpAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Enabled property
ms.assetid: 870fd4d0-6c77-462a-b480-d42eb044b2e7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 585601724ebc34139c554bde6c85d14028e5e05e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485217"
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Enabled 속성(ServerNetworkProtocolIpAddress 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  IP 주소가 설정되었는지 여부를 지정하는 부울 속성을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 인스턴스의 네트워크 프로토콜에 대 한 IP 주소를 나타내는 [ServerNetworkProtocolIPAdress 클래스](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 Ip 주소를 사용할 수 있는지 여부를 지정 하는 부울 값입니다. IP 주소를 사용 하는 경우 **true** 이 고, ip 주소를 사용 하지 않도록 설정 된 경우에는 **false** 입니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

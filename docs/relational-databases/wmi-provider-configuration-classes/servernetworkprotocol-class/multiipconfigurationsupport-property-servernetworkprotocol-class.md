---
title: MultiIpConfigurationSupport 속성 (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0ff19a1a89c301b018a9231ca8c98277d6a55e43
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888733"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>MultiIpConfigurationSupport 속성(ServerNetworkProtocol 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서버 네트워크 프로토콜에서 여러 개의 IP 주소를 지원하는지 여부를 지정하는 부울 속성을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 인스턴스에서 사용 하는 네트워크 프로토콜을 나타내는 [Protocolname 속성 (ServerNetworkProtocol 클래스)](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md) 개체입니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서버 네트워크 프로토콜에서 여러 ip 주소를 지원 하는지 여부를 지정 하는 부울 값: 서버 네트워크 프로토콜에서 여러 개의 ip 주소를 지원 하면 **true** 이 고, 여러 ip 주소가 서버 네트워크 프로토콜에서 지원 되지 않는 경우 **false** 입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

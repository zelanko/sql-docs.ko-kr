---
description: SupportAlias 속성(ClientNetworkProtocol 클래스)
title: SupportAlias 속성 (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SupportAlias Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 456f4bfd3d2051bff614d1d65710366ea39b08b5
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91888988"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>SupportAlias 속성(ClientNetworkProtocol 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [Setordervalue 메서드 (ClientNetworkProtocol 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) 에서 지정한 현재 네트워크 프로토콜이 별칭을 지원 하는지 여부를 지정 하는 부울 속성을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SupportAlias [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [클라이언트에서 사용하는 네트워크 프로토콜을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 클라이언트 네트워크 프로토콜이 별칭을 지원하는지 여부를 지정하는 부울 값입니다.  
  
 True인 경우 클라이언트 네트워크 프로토콜이 별칭을 지원합니다.  
  
 False인 경우 클라이언트 네트워크 프로토콜이 별칭을 지원하지 않습니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  

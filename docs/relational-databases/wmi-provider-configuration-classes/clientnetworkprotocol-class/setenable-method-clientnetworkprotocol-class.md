---
description: SetEnable 메서드(ClientNetworkProtocol 클래스)
title: SetEnable 메서드 (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetEnable Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetEnable method
ms.assetid: a66c756a-1311-4f4a-8088-818f8ed90056
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dcc745710132ea85b7027152900b7d693df37aab
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91889039"
---
# <a name="setenable-method-clientnetworkprotocol-class"></a>SetEnable 메서드(ClientNetworkProtocol 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [클라이언트 프로토콜 구성](../../../database-engine/configure-windows/configure-client-protocols.md)에서 지정한 클라이언트 네트워크 프로토콜을 사용 하도록 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetEnableMethod()  
```  
  
## <a name="parts"></a>부분  
 *object*  
 클라이언트에서 사용 하는 네트워크 프로토콜을 나타내는 [Clientnetworkprotocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](../../../database-engine/configure-windows/configure-client-protocols.md)  
  

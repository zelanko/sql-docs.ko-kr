---
description: SetEnable 메서드(ServerNetworkProtocol 클래스)
title: SetEnable 메서드 (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetEnable Method (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetEnable method
ms.assetid: a287950b-086f-4b6d-a2d8-4d3973bd1b21
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 971aa14a2ba3fa357f15a5b8d53b51dfc7b36492
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545441"
---
# <a name="setenable-method-servernetworkprotocol-class"></a>SetEnable 메서드(ServerNetworkProtocol 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서버 네트워크 프로토콜을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetEnable()  
```  
  
## <a name="parts"></a>부분  
 *object*  
 인스턴스에서 사용 하는 네트워크 프로토콜을 나타내는 [Servernetworkprotocol 클래스](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md) 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

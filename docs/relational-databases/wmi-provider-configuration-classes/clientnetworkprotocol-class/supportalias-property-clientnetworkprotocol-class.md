---
title: "SupportAlias 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SupportAlias Property (ClientNetworkProtocol Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f83e28362866b3a622b0e15670445d4e88878013
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>SupportAlias 속성(ClientNetworkProtocol 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]현재 네트워크에 지정 된 프로토콜 있는지 여부를 지정 하는 부울 속성을 가져옵니다는 [SetOrderValue 메서드 (ClientNetworkProtocol 클래스)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) 별칭을 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SupportAlias [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 [클라이언트에서 사용하는 네트워크 프로토콜을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 클라이언트 네트워크 프로토콜이 별칭을 지원하는지 여부를 지정하는 부울 값입니다.  
  
 True인 경우 클라이언트 네트워크 프로토콜이 별칭을 지원합니다.  
  
 False인 경우 클라이언트 네트워크 프로토콜이 별칭을 지원하지 않습니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  

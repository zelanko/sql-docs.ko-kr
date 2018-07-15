---
title: SupportAlias 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SupportAlias Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
caps.latest.revision: 16
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bd18c837ca94878887bdf30fc0412dddff59cb83
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37327553"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>SupportAlias 속성(ClientNetworkProtocol 클래스)
  현재 네트워크에 지정 된 프로토콜 여부를 지정 하는 부울 속성을 가져옵니다 합니다 [SetOrderValue 메서드 (ClientNetworkProtocol 클래스)](clientnetworkprotocol-class.md) 별칭을 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [클라이언트에서 사용하는 네트워크 프로토콜을 나타내는](clientnetworkprotocol-class.md) ClientNetworkProtocol 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 클라이언트 네트워크 프로토콜이 별칭을 지원하는지 여부를 지정하는 부울 값입니다.  
  
 True인 경우 클라이언트 네트워크 프로토콜이 별칭을 지원합니다.  
  
 False인 경우 클라이언트 네트워크 프로토콜이 별칭을 지원하지 않습니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  

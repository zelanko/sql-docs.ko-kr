---
title: 번호 Off지연과 지연 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- NumberOfFlags Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: 7a656644-2154-419f-9787-99877f597770
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9a47f6e17a85fdf9cec169a611b9fe205ba02543
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63192038"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>NumberOfFlags 속성(ClientNetworkProtocol 클래스)
  [Setordervalue 메서드 (ClientNetworkProtocol 클래스)](clientnetworkprotocol-class.md)에서 지정한 클라이언트 네트워크 프로토콜에 필요한 플래그 옵션의 수를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [클라이언트에서 사용하는 네트워크 프로토콜을 나타내는](clientnetworkprotocol-class.md) ClientNetworkProtocol 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `Uint32` 속성에서 참조하는 클라이언트 네트워크 프로토콜에 필요한 플래그 옵션의 수를 지정하는 `OrderValue` 값입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 프로토콜 구성](https://technet.microsoft.com/library/ms181035.aspx)  
  
  

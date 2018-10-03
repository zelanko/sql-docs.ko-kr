---
title: NumberOfFlags 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
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
ms.openlocfilehash: 6be2a4a4e85b3d92cb44db8783dfa7c12e595f87
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057103"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>NumberOfFlags 속성(ClientNetworkProtocol 클래스)
  지정한 클라이언트 네트워크 프로토콜에 필요한 플래그 옵션의 수를 가져옵니다 합니다 [SetOrderValue 메서드 (ClientNetworkProtocol 클래스)](clientnetworkprotocol-class.md)합니다.  
  
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
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  

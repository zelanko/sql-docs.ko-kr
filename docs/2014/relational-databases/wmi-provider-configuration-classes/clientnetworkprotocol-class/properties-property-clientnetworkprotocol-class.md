---
title: Properties 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
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
- Properties Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4882f26e1f74fd68e67f14172482bcc674d1b06e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088111"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Properties 속성(ClientNetworkProtocol 클래스)
  [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)에서 지정한 현재 클라이언트 네트워크 프로토콜과 연결된 속성을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [클라이언트에서 사용하는 네트워크 프로토콜을 나타내는](clientnetworkprotocol-class.md) ClientNetworkProtocol 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 배열을 [ClientNetworkProtocolProperty 클래스](../clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) 에서 참조 되는 현재 클라이언트 네트워크 프로토콜에서 지 원하는 속성을 나타내는 개체는 `OrderValue` 속성입니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
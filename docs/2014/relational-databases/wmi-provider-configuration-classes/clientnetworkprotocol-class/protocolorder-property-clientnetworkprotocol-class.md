---
title: ProtocolOrder 속성 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProtocolOrder Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0a0043e5a894e3f3f1b778a6f42fe6e3bacbbc78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192887"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 속성(ClientNetworkProtocol 클래스)
  현재 참조 되는 클라이언트의 순서 번호를 지정 된 대로 네트워크 프로토콜을 가져옵니다 합니다 [SetOrderValue 메서드 (ClientNetworkProtocol 클래스)](clientnetworkprotocol-class.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [ClientNetworkProtocol 클래스](clientnetworkprotocol-class.md) 사용 되는 네트워크 프로토콜을 나타내는 개체를 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 메서드에서 설정한 현재 참조되는 클라이언트 네트워크 프로토콜의 순서 번호를 지정하는 `OrderValue` 값입니다. 클라이언트 네트워크 프로토콜이 해제된 경우 이 값은 0입니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 프로토콜 구성](https://technet.microsoft.com/library/ms181035.aspx)   
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://technet.microsoft.com/library/ms181035.aspx)  
  
  

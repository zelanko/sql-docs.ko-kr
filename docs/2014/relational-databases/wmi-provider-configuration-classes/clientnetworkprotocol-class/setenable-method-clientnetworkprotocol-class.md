---
title: SetEnable 메서드 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetEnable Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: a66c756a-1311-4f4a-8088-818f8ed90056
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1aa192f2dc78a424b1d4c8792044caac0934173a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62826723"
---
# <a name="setenable-method-clientnetworkprotocol-class"></a>SetEnable 메서드(ClientNetworkProtocol 클래스)
  [클라이언트 프로토콜 구성](https://technet.microsoft.com/library/ms181035.aspx)에서 지정한 클라이언트 네트워크 프로토콜을 사용 하도록 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetEnableMethod()  
  
```  
  
## <a name="parts"></a>부분  
 *개체가*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 사용 하는 네트워크 프로토콜을 나타내는 [clientnetworkprotocol 클래스](clientnetworkprotocol-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 
  `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://technet.microsoft.com/library/ms181035.aspx)  
  
  

---
title: SetEnable 메서드 (ServerNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetEnable Method (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: a287950b-086f-4b6d-a2d8-4d3973bd1b21
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f3dee294e84ebe0fa8577630886ee00255e928ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63055703"
---
# <a name="setenable-method-servernetworkprotocol-class"></a>SetEnable 메서드(ServerNetworkProtocol 클래스)
  서버 네트워크 프로토콜을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetEnable()  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [ServerNetworkProtocol 클래스](servernetworkprotocol-class.md) 인스턴스에서 사용 하는 네트워크 프로토콜을 나타내는 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

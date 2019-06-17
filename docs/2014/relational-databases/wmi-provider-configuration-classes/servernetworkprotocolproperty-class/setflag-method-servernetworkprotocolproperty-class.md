---
title: SetFlag 메서드 (ServerNetworkProtocolProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetFlag Method (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetFlag method
ms.assetid: 95288931-8eb1-4477-ad80-619cf7073e61
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 95682cc34f67a0d65f62afdc52ec09c5209e3ba4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642678"
---
# <a name="setflag-method-servernetworkprotocolproperty-class"></a>SetFlag 메서드(ServerNetworkProtocolProperty 클래스)
  참조된 속성의 플래그를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetFlag(  
BoolValue  
)  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [ServerNetworkProtocolProperty 클래스] servernetworkprotocolproperty-class.md) 인스턴스의 네트워크 프로토콜의 특성을 나타내는 개체 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*BoolValue*|플래그의 새 값을 지정하는 부울 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

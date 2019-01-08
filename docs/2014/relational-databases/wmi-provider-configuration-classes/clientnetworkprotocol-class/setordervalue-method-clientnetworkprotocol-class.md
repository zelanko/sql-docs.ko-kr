---
title: SetOrderValue 메서드 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetOrderValue Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetOrderValue method
ms.assetid: 15f693fd-37f6-41d9-9dab-d2c93db19895
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b06773049204b126a37e21ce8c070f11666f19df
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373125"
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>SetOrderValue 메서드(ClientNetworkProtocol 클래스)
  지정된 순서 값을 가진 프로토콜을 클라이언트 프로토콜 목록에서 선택합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetOrderValue(  
OrderValue  
)  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [클라이언트에서 사용하는 네트워크 프로토콜을 나타내는](clientnetworkprotocol-class.md) ClientNetworkProtocol 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*OrderValue*|순서 값을 설정하는 `int32` 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 프로토콜 속성(순서 탭)](https://technet.microsoft.com/library/ms187884.aspx)  
  
  

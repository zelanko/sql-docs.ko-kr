---
title: SetNumericalValue 메서드 (ServerNetworkProtocolProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetNumericalValue Method (ServerNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: b3b4bce8-9d9e-4ccb-a223-0454281353b0
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0d61c99f046e1030ef00925e13bcd39b6abeddb0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62660510"
---
# <a name="setnumericalvalue-method-servernetworkprotocolproperty-class"></a>SetNumericalValue 메서드(ServerNetworkProtocolProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  참조된 속성의 숫자 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetNumericalValue(NumValue)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [ServerNetworkProtocolProperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) 인스턴스의 네트워크 프로토콜의 특성을 나타내는 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*NumValue*|A **uint32** 현재 속성의 새 값을 지정 하는 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

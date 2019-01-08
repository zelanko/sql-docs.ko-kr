---
title: SetBoolValue 메서드 (SqlServiceAdvancedProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- SetBoolValue Method (SqlServiceAdvancedProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetBoolValue method
ms.assetid: 5252b439-fce5-446a-8e57-99e3054bee69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 302ac36150d21dfecca1e6c6edfbcf6fd86c42f0
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356448"
---
# <a name="setboolvalue-method-sqlserviceadvancedproperty-class"></a>SetBoolValue 메서드(SqlServiceAdvancedProperty 클래스)
  속성의 부울 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetBoolValue [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 고급 속성을 나타내는 [SqlServiceAdvancedProperty 클래스](../wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*BoolValue*|고급 속성의 값을 지정하는 부울 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 속성을 부울 값으로 설정하려면 속성 값 형식이 부울이어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

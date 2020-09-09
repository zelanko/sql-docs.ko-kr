---
description: SetNumericalValue 메서드(SqlServiceAdvancedProperty 클래스)
title: SetNumericalValue 메서드 (SqlServiceAdvancedProperty)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetNumericalValue Method (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: 950ed1e8-0538-4db4-807c-a2c36f43cf6b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a3c9ccf43a8edd0298de5d9d7ecbcfbbcfea3c5e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542775"
---
# <a name="setnumericalvalue-method-sqlserviceadvancedproperty-class"></a>SetNumericalValue 메서드(SqlServiceAdvancedProperty 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  속성의 숫자 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetNumericalValue(NumValue)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 고급 속성을 나타내는 [SqlServiceAdvancedProperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*NumValue*|고급 속성의 값을 지정하는 **uint32** 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 속성을 숫자 값으로 설정하려면 속성 값 형식이 숫자여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

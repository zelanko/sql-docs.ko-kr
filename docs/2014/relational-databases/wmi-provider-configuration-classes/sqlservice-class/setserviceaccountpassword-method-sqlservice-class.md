---
title: SetServiceAccountPassword 메서드 (SqlService 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetServiceAccountPassword Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 41823ebcbad3f545a8b516b3fad457230d3fdf8e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067882"
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>SetServiceAccountPassword 메서드(SqlService 클래스)
  참조된 서비스가 실행되는 계정의 암호를 수정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetServiceAccountPassword(  
AccountOldPassword , ServiceStartPassword  
)  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](sqlservice-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *AccountOldPassword*  
 계정의 기존 암호를 지정하는 문자열 값입니다.  
  
 *ServiceStartPassword*  
 계정의 새 암호를 지정하는 문자열 값입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  

---
title: StopService 메서드 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StopService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StopService method
ms.assetid: ef8e1856-4930-417a-8f52-be470fd3f15c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a8fe68790b30ffdc54e9f30e4f85675eb595d09e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880563"
---
# <a name="stopservice-method-sqlservice-class"></a>StopService 메서드(SqlService 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서비스를 중지된 상태로 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.StopService()  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 **ResumeService** 요청이 수락되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

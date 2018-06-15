---
title: ErrorControl 속성 (SqlService 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e787de01cbcde080706d4a3bd569fb365cc17394
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33010720"
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl 속성(SqlService 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  시스템을 시작할 때 서비스가 시작되지 않은 경우 오류의 심각도를 가져오거나 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 시스템을 시작할 때 서비스가 시작되지 않은 경우 보고된 오류 심각도를 지정하는 문자열 값입니다. 다음 표에서는 가능한 값을 보여 줍니다.  
  
 무시  
 사용자에게 오류를 알리지 않습니다.  
  
 Normal  
 사용자에게 오류를 알립니다.  
  
 심각  
 마지막으로 성공한 올바른 구성으로 시스템을 다시 시작합니다.  
  
 심각  
 올바른 구성으로 시스템을 다시 시작합니다.  
  
 Unknown  
 심각도를 알 수 없습니다.  
  
## <a name="remarks"></a>주의  
 이 값은 오류가 발생할 때 시작 프로그램에서 수행하는 동작을 나타냅니다. 모든 오류는 컴퓨터 시스템에 기록됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [서비스 시작 및 중지](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

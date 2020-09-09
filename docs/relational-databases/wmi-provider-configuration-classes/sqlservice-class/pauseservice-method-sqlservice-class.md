---
description: PauseService 메서드(SqlService 클래스)
title: PauseService 메서드 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PauseService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PauseService method
ms.assetid: 5c3a8feb-58b8-4385-b4c8-bf33cf4d276d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9657d824326447ebf0f395e79c274173ec57cc20
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542904"
---
# <a name="pauseservice-method-sqlservice-class"></a>PauseService 메서드(SqlService 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서비스를 일지 중지된 상태로 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.PauseService()  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 uint32 값으로, 0은 서비스가 중지되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

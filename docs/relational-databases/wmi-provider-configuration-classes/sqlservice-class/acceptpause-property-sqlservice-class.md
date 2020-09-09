---
description: AcceptPause 속성(SqlService 클래스)
title: AcceptPause 속성 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptPause Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptPause property
ms.assetid: 4339e903-35ee-4395-b005-ca58b3a24a84
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5b86054eb6ce914a094f537374611ff71180f156
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550906"
---
# <a name="acceptpause-property-sqlservice-class"></a>AcceptPause 속성(SqlService 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서비스를 일시 중지할 수 있는지 여부를 지정하는 부울 속성 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.AcceptPause [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서비스를 일시 중지할 수 있는지 여부를 지정하는 부울 값입니다. **true** 인 경우 서비스를 일시 중지할 수 있고 **false** 인 경우 서비스를 일시 중지할 수 없습니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

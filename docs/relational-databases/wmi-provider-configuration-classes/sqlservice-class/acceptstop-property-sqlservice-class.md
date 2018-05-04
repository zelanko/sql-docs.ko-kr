---
title: AcceptStop 속성 (SqlService 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AcceptStop Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 57e8a60b431ad0a5f24ad01d3d3536642fe3887a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop 속성(SqlService 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  서비스를 중지할 수 있는지 여부를 지정하는 부울 속성 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.AcceptStop [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 A [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 서비스를 나타내는 개체  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서비스를 중지할 수 있는지 여부를 지정 하는 부울 값: **true** 서비스를 중지할 경우 또는 **false** 서비스를 중지할 수 없습니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [서비스 시작 및 중지](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

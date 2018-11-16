---
title: AcceptStop 속성 (SqlService 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptStop Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 26889228181b16c7ea58560708766d048b939f0d
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656692"
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop 속성(SqlService 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  서비스를 중지할 수 있는지 여부를 지정하는 부울 속성 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.AcceptStop [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 서비스를 나타내는 개체  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서비스를 중지할 수 있는지 여부를 지정 하는 부울 값: **true** 서비스를 중지할 경우 또는 **false** 서비스를 중지할 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

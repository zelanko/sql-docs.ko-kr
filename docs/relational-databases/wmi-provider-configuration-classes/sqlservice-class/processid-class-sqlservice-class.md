---
title: ProcessId 클래스 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProcessId Class (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8418bd70e3aa2b28e0274bec63c312aba2849b84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73657072"
---
# <a name="processid-class-sqlservice-class"></a>ProcessId 클래스(SqlService 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  서비스를 고유하게 식별하는 시스템 프로세스 ID를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ProcessId [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체가*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 프로세스를 고유 하 게 식별 하는 ID를 지정 하는 **uint32** 값입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="example"></a>예제  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

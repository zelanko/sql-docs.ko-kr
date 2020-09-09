---
description: ProcessId 클래스(SqlService 클래스)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d4e6ceb18ecda885481860bf9889143bccfd0ed6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540042"
---
# <a name="processid-class-sqlservice-class"></a>ProcessId 클래스(SqlService 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서비스를 고유하게 식별하는 시스템 프로세스 ID를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ProcessId [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
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
  
  

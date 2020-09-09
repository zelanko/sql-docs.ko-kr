---
description: DisplayName 속성(SqlService 클래스)
title: DisplayName 속성 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- DisplayName Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- DisplayName property
ms.assetid: 49c408aa-6eb4-45cd-8d5c-60f065f24f5c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a3235e2d4f1491ccd7932f1ebb76e2b7eacf9b51
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550828"
---
# <a name="displayname-property-sqlservice-class"></a>DisplayName 속성(SqlService 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서비스의 표시 이름을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.DisplayName [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서비스의 표시 이름을 지정하는 문자열 값입니다.  
  
## <a name="remarks"></a>설명  
 이 문자열의 최대 길이는 256자입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자에서는 이름의 대/소문자가 유지되지만 표시 이름을 비교할 때는 항상 대/소문자가 무시됩니다.  
  
## <a name="example"></a>예제  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

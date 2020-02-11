---
title: 종속성 속성 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Dependencies Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Dependencies property
ms.assetid: 92d54b7e-de2f-4978-b601-0196e37cbb41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 993c922562773648aac5460116ba6e343a72132f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73659282"
---
# <a name="dependencies-property-sqlservice-class"></a>Dependencies 속성(SqlService 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  참조된 서비스에 종속된 서비스의 목록을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Dependencies [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체가*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 참조된 서비스에 종속된 서비스의 목록을 포함하는 string[] 형식의 배열입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

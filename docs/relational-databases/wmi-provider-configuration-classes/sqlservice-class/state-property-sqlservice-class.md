---
title: State 속성 (SqlService 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- State Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 06193b774484afd6e6f7f47f286498c0698ab7c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094736"
---
# <a name="state-property-sqlservice-class"></a>State 속성(SqlService 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  서비스의 현재 상태를 가져오거나 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.State [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서비스의 상태를 지정하는 uint32 값입니다.  
  
 다음 값 중 하나일 수 있습니다.  
  
 1  
 중지됨. 서비스가 중지되었습니다.  
  
 2  
 시작 보류 중. 서비스가 시작되기를 기다리고 있습니다.  
  
 3  
 중지 보류 중. 서비스가 중지되기를 기다리고 있습니다.  
  
 4  
 실행 중. 서비스가 실행되고 있습니다.  
  
 5  
 계속 보류 중. 서비스가 계속되기를 기다리고 있습니다.  
  
 6  
 일시 중지 보류 중. 서비스가 일시 중지되기를 기다리고 있습니다.  
  
 7  
 일시 중지됨 서비스가 일시 중지되었습니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>관련 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  

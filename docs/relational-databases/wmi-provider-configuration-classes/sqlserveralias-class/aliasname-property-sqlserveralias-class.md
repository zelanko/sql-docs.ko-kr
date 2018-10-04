---
title: AliasName 속성 (SqlServerAlias 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- AliasName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AliasName property
ms.assetid: 5c4c88f3-c1cf-471a-9d91-f47657933e2f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 53c50db2baeeb894f41cf84274af3e7f7a24699b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776881"
---
# <a name="aliasname-property-sqlserveralias-class"></a>AliasName 속성(SqlServerAlias 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  서버 연결 별칭의 이름을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.AliasName [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [별칭을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) SqlServerAlias 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서버 연결 별칭의 이름을 지정하는 **string** 값입니다.  
  
## <a name="remarks"></a>Remarks  
  

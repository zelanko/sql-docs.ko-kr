---
title: "ServerName 속성 (SqlServerAlias 클래스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ServerName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ServerName property
ms.assetid: 58c82b19-b548-42fa-9c5a-059b606da097
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0940ecd06f1c1c4ad7b3a0fc43e4323c46067278
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="servername-property-sqlserveralias-class"></a>ServerName 속성(SqlServerAlias 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
서버 연결 별칭에서 지정한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.ServerName [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체*  
 [별칭을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) SqlServerAlias 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서버 연결 별칭에서 참조하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정하는 문자열 값입니다.  
  
## <a name="remarks"></a>주의  
  

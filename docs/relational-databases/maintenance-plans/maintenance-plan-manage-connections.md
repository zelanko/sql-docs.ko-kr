---
title: 유지 관리 계획(연결 관리) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.connections.f1
ms.assetid: 95ad9375-6584-423e-b9de-0e86782f8017
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a388792d24ce033dce0ffb4c6f0120a6ea341ae0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115957"
---
# <a name="maintenance-plan-manage-connections"></a>유지 관리 계획(연결 관리)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **연결 관리** 대화 상자를 사용하여 유지 관리 계획에서 사용하는 연결의 속성을 지정할 수 있습니다. 유지 관리 계획을 만들면 해당 계획을 만든 서버에 대한 로컬 연결이 생성됩니다. 이 연결을 사용하여 이 로컬 연결에 대한 태스크를 수행하는 작업을 만들 수 있습니다. 필요하면 **연결 관리** 대화 상자를 사용하여 연결을 추가합니다. 추가 연결을 구성하면 각 태스크의 연결 상자에 해당 연결이 나타납니다.  
  
## <a name="options"></a>옵션  
 **Server**  
 서버 인스턴스입니다.  
  
 **인증**  
 Windows 인증으로 연결되는지 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증으로 연결되는지 나타냅니다.  

> [!IMPORTANT]  
> 패키지는 **ServerStorage**로 설정된 해당 **ProtectionLevel**로 **msdb** 데이터베이스에 저장되므로 *SQL Server 인증*이 사용될 때 암호는 **msdb**에서 암호화되지 않습니다. *msdb*가 보호되는 한 **SQL Server 인증**을 사용할 수 있지만 *Windows 인증*을 사용하는 것이 좋습니다.

## <a name="see-also"></a>참고 항목  
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  

---
title: 가용성 그룹 상태에 그룹 정책 사용
description: Always On 대시보드가 가용성 그룹 상태에 대한 정보를 제공하는 데 사용하는 그룹 시스템 정책을 보는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 26bf8f71-c2b8-45ef-b3a3-372b96c9e6e3
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a48450322a8552720a119ea325ed720669fe5a8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75245648"
---
# <a name="evaluate-health-of-the-always-on-availability-group-using-group-policies"></a>그룹 정책을 사용하여 Always On 가용성 그룹의 상태 평가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Always On 가용성 그룹 시스템 정책은 가용성 그룹 상태에서 사용자에게 정보를 제공하기 위해 Always On 대시보드에서 사용됩니다. 가용성 그룹 운영 문제의 초기 문제 해결에 매우 유용합니다. 이러한 정책은 Always On 대시보드를 사용자 지정하거나 원하는 상태 정보를 보고하기 위해 즉시 실행하도록 확장되고 사용될 수 있습니다.  
  
 가용성 그룹에 대한 14개의 시스템 정책이 있습니다. 각 정책에 대한 자세한 내용은 [Always On 가용성 그룹의 운영 문제에 대한 Always On 정책(SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md)을 참조하세요.  
  
## <a name="view-or-evaluate-availability-groups-system-policies"></a>가용성 그룹 시스템 정책 보기 또는 평가  
 SSMS(SQL Server Management Studio)에서 가용성 그룹 시스템 정책을 보거나 실행하려면 다음을 수행합니다.  
  
1.  **개체 탐색기**에서 **관리**, **정책 관리**, **정책**을 차례로 확장한 다음 **시스템 정책**을 확장합니다.  
  
2.  정책 중 하나를 마우스 오른쪽 단추로 클릭하고 **평가**를 클릭합니다. 선택한 정책을 평가하려는 경우 수행됩니다. **대상 세부 정보** 상자의 **보기**를 클릭하여 평가 결과의 세부 정보를 볼 수 있습니다.  
  
3.  모든 가용성 그룹 시스템 정책을 보려면 **페이지 선택** 창에서 **정책 선택**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 [Always On 상태 모델, 파트 2: 상태 모델 확장](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)   
  
  

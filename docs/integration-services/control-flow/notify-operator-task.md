---
title: 운영자에게 알림 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.notifyoperatortask.f1
helpviewer_keywords:
- Notify Operator task
- notifications [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 6c816c68-c6d6-44e4-bb34-c8e060a958a1
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e5847d578c38c482a152f13a0ff41ad7907e65a8
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40411059"
---
# <a name="notify-operator-task"></a>운영자에게 알림 태스크
  운영자에게 알림 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 운영자에게 알림 메시지를 보냅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 운영자는 전자 알림을 받을 수 있는 사람 또는 그룹의 별칭입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 운영자에 대한 자세한 내용은 [운영자](../../ssms/agent/operators.md)를 참조하세요.  
  
 운영자에게 알림 태스크를 사용하면 패키지가 메일, 호출기 또는 **net send**를 통해 한 명 이상의 운영자에게 알림을 보낼 수 있습니다. 각 운영자는 다른 방법으로 알림을 받을 수 있습니다. 예를 들어 OperatorA는 메일과 호출기를 통해 알림을 받고 OperatorB는 호출기와 **net send**를 통해 알림을 받습니다. 태스크에서 알림을 받는 운영자는 운영자에게 알림 태스크의 **OperatorNotify** 컬렉션 멤버여야 합니다.  
  
 운영자에게 알림 태스크는 Transact-SQL 문이나 DBCC 명령을 캡슐화하지 않는 유일한 데이터베이스 유지 관리 태스크입니다.  
  
## <a name="configuration-of-the-notify-operator-task"></a>운영자에게 알림 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [운영자에게 알림 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  

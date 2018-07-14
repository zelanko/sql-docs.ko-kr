---
title: '2 단원: 일정에 따라 최선의 구현 방법 정책 평가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 37ffad63-d6db-4609-8deb-786200659554
caps.latest.revision: 4
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: bfdad3793673e24ddf87d504ab71c96c0bac16f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196603"
---
# <a name="lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis"></a>2단원: 일정에 따라 최선의 구현 방법 정책 평가
  하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대해 최선의 구현 방법 정책에 대한 예약된 평가를 구성할 수 있습니다. 일정에 따라 최선의 구현 방법 정책을 실행하도록 구성하려면 정책을 대상 인스턴스로 가져와야 합니다.  
  
 예약된 정책을 여러 서버에 배포하려면 정책을 하나의 인스턴스로 가져와 각 정책에 대한 일정을 구성하고 예약된 정책을 폴더로 내보낸 다음 등록된 서버를 통해 예약된 정책을 대상 인스턴스에 배포합니다.  
  
> [!IMPORTANT]  
>  대상 인스턴스는 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 이상 버전을 실행 중이어야 합니다. 자동화를 수행하려면 정책을 인스턴스에 로컬로 저장해야 합니다. 이 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이전 버전인 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 지원되지 않습니다.  
  
 이 단원에서는 다음을 수행합니다.  
  
-   최선의 구현 방법 정책을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스로 가져옵니다.  
  
-   일정에 따라 정책을 실행하도록 구성합니다.  
  
-   예약된 최선의 구현 방법 정책을 등록된 서버를 통해 여러 인스턴스에 배포합니다.  
  
 이 단원에서는 다음 항목을 다룹니다.  
  
-   [단일 인스턴스로 정책 가져오기](../../2014/tutorials/import-the-policies-to-a-single-instance.md)  
  
-   [정책 예약](../../2014/tutorials/schedule-the-policies.md)  
  
-   [여러 인스턴스에 예약된 정책 배포](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
## <a name="see-also"></a>관련 항목  
 [중앙 관리 서버를 사용하여 여러 서버 관리](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  

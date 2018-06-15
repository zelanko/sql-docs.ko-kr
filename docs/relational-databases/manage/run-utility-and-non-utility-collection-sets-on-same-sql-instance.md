---
title: 동일한 SQL 인스턴스에서 유틸리티 및 유틸리티 이외의 컬렉션 집합 실행 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ed0321c8b1621bfb9a011e7a3948f8361a6e7d2e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32942218"
---
# <a name="run-utility-and-non-utility-collection-sets-on-same-sql-instance"></a>동일한 SQL 인스턴스에서 유틸리티 및 유틸리티 이외의 컬렉션 집합 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 이외의 컬렉션 집합과 함께 사용하는 것이 가능합니다. 즉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 멤버이면 다른 컬렉션 집합으로 모니터링할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록하는 동안에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 이외의 데이터 컬렉션 기능을 해제해야 합니다.  
  
 UCP를 인스턴스에 등록한 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 이외의 컬렉션 집합을 다시 시작할 수 있습니다. 그러나 관리되는 인스턴스의 모든 컬렉션 집합은 해당 데이터를 UMDW(유틸리티 관리 데이터 웨어하우스)로 업로드합니다. UMDW의 파일 이름은 sysutility_mdw입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 컬렉션 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 이외의 컬렉션 집합과 함께 실행하려면 다음 사항을 고려하십시오.  
  
-   컬렉션 집합을 함께 사용할 수 있습니다.  
  
-   인스턴스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록하는 동안에는 기존 데이터 수집기를 해제해야 합니다.  
  
-   유효성 검사 요구 사항을 통과하려면 UCP를 만들기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서, 그리고 이를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 다음 저장 프로시저를 실행해야 합니다.  
  
    ```  
    exec msdb.dbo.sp_syscollector_set_warehouse_database_name NULL  
    exec msdb.dbo.sp_syscollector_set_warehouse_instance_name NULL  
    ```  
  
     UCP 만들기 마법사나 관리되는 인스턴스 추가 마법사를 시작하기 전에 이러한 저장 프로시저를 실행하지 않으면 작업이 실패합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에서 모든 컬렉션 집합에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]유틸리티 UMDW(sysutility_mdw)를 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [유틸리티 제어 지점 데이터 웨어하우스 구성&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  

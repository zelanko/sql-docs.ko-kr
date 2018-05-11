---
title: 관리되는 SQL Server에서 유틸리티 컬렉션에 대한 프록시 계정 변경 | Microsoft 문서
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
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 18783eadd178345772c2ef861e202ba512aaf9b2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="change-proxy-account-for-utility-collection-on--managed-sql-server"></a>관리되는 SQL Server에서 유틸리티 컬렉션에 대한 프록시 계정 변경
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]관리 인스턴스의 유틸리티 컬렉션 집합에 대한 프록시 계정을 변경하는 방법에 대해 설명합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>SQL Server의 관리 인스턴스에서 유틸리티 컬렉션 집합에 대한 프록시 계정을 변경하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스를 제거합니다.  
  
    -   SSMS의 **유틸리티 탐색기** 에서 **관리되는 인스턴스** 노드를 클릭합니다.  
  
    -   **유틸리티 탐색기** 목록 뷰에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 마우스 오른쪽 단추로 클릭하고 **관리되는 인스턴스 제거…**를 선택합니다. 자세한 내용은 [SQL Server 유틸리티에서 SQL Server 인스턴스 제거](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)를 참조하세요.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록합니다.  
  
    -   SSMS의 **유틸리티 탐색기** 에서 **관리되는 인스턴스** 노드를 마우스 오른쪽 단추로 클릭하고 **관리되는 인스턴스 추가…**를 선택합니다.  
  
    -   표시되는 메시지에 따라 마법사를 완료하여 새 프록시 계정을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 유틸리티 문제 해결](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  

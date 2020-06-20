---
title: SQL Server (SQL Server 유틸리티) Managed Instance에서 유틸리티 컬렉션 집합에 대 한 프록시 계정을 변경 합니다. Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c1f78c711b19b742176517962a45618f112a67cc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023802"
---
# <a name="change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server-sql-server-utility"></a>SQL Server 관리되는 인스턴스의 유틸리티 컬렉션 집합을 위한 프록시 계정 변경(SQL Server 유틸리티)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 관리되는 인스턴스의 유틸리티 컬렉션 집합에 대한 프록시 계정을 변경하는 방법에 대해 설명합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>SQL Server의 관리되는 인스턴스에서 유틸리티 컬렉션 집합에 대한 프록시 계정을 변경하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스를 제거합니다.  
  
    -   SSMS의 **유틸리티 탐색기**에서 **관리되는 인스턴스** 노드를 클릭합니다.  
  
    -   **유틸리티 탐색기** 목록 뷰에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 마우스 오른쪽 단추로 클릭하고 **Managed Instance 제거...** 를 선택합니다. 자세한 내용은 [SQL Server 유틸리티에서 SQL Server 인스턴스 제거](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)를 참조하세요.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록합니다.  
  
    -   SSMS의 **유틸리티 탐색기**에서 **Managed Instance** 노드를 마우스 오른쪽 단추로 클릭하고 **Managed Instance 추가...** 를 선택합니다.  
  
    -   표시되는 메시지에 따라 마법사를 완료하여 새 프록시 계정을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](sql-server-utility-features-and-tasks.md)   
 [SQL Server 유틸리티 문제 해결](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  

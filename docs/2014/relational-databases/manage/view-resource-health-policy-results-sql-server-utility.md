---
title: 리소스 상태 정책 결과 보기(SQL Server 유틸리티) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fe09be4c3b91471edda0fcf2e4a0af8ba2092aa5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37164254"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>리소스 상태 정책 결과 보기(SQL Server 유틸리티)
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 의 유틸리티 대시보드를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 및 데이터 계층 응용 프로그램의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 유틸리티 리소스 매개 변수를 볼 수 있습니다. 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>SQL Server 유틸리티 리소스 상태 정책 결과 보기  
  
1.  유틸리티 탐색기 탐색 창을 보려면 SSMS( [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] )에서 **보기**를 클릭하고 **유틸리티 탐색기** 를 선택합니다. 내용 창을 보려면 **보기**를 클릭하고 **유틸리티 탐색기 내용**을 클릭합니다.  
  
2.  탐색 창에서 ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")**유틸리티에 연결**을 클릭합니다. UCP(유틸리티 제어 지점)를 만들지 않았거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 또는 데이터 계층 응용 프로그램을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 유틸리티에 등록하지 않은 경우 [SQL Server 유틸리티 기능 및 작업](sql-server-utility-features-and-tasks.md)을 참조하세요.  
  
3.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 및 데이터 계층 응용 프로그램의 요약 데이터를 보려면 UCP 노드를 클릭합니다(새로 고치려면 마우스 오른쪽 단추 클릭). 대시보드 데이터가 내용 창에 표시됩니다.  
  
4.  **의 관리되는 인스턴스의 목록 뷰 데이터를 보려면** 관리되는 인스턴스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 노드를 클릭합니다(새로 고치려면 마우스 오른쪽 단추 클릭). 목록 뷰 데이터가 내용 창에 표시됩니다.  
  
5.  데이터 계층 응용 프로그램의 목록 뷰를 보려면 **배포된 데이터 계층 응용 프로그램** 노드를 클릭합니다(새로 고치려면 마우스 오른쪽 단추 클릭). 목록 뷰 데이터가 내용 창에 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 유틸리티 기능 및 태스크](sql-server-utility-features-and-tasks.md)   
 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [배포된 데이터 계층 응용 프로그램 세부 정보&#40;SQL Server 유틸리티&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [관리되는 인스턴스 세부 정보&#40;SQL Server 유틸리티&#41;](../../database-engine/managed-instance-details-sql-server-utility.md)   
 [유틸리티 관리&#40;SQL Server 유틸리티&#41;](../../database-engine/utility-administration-sql-server-utility.md)  
  
  

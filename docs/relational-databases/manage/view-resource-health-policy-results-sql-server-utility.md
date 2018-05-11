---
title: 리소스 상태 정책 결과 보기(SQL Server 유틸리티) | Microsoft 문서
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
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 22f07e28b8b047074424d3480d026b7c5b73cf5e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>리소스 상태 정책 결과 보기(SQL Server 유틸리티)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 유틸리티 대시보드를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 및 데이터 계층 응용 프로그램의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 리소스 매개 변수를 볼 수 있습니다. 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>SQL Server 유틸리티 리소스 상태 정책 결과 보기  
  
1.  유틸리티 탐색기 탐색 창을 보려면 SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )에서 **보기**를 클릭하고 **유틸리티 탐색기** 를 선택합니다. 내용 창을 보려면 **보기**를 클릭하고 **유틸리티 탐색기 내용**을 클릭합니다.  
  
2.  탐색 창에서 ![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")**유틸리티에 연결**을 클릭합니다. UCP(유틸리티 제어 지점)를 만들지 않았거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 데이터 계층 응용 프로그램을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록하지 않은 경우 [SQL Server 유틸리티 기능 및 작업](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)을 참조하세요.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스 및 데이터 계층 응용 프로그램의 요약 데이터를 보려면 UCP 노드를 클릭합니다(새로 고치려면 마우스 오른쪽 단추 클릭). 대시보드 데이터가 내용 창에 표시됩니다.  
  
4.  **의 관리되는 인스턴스의 목록 뷰 데이터를 보려면** 관리되는 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 노드를 클릭합니다(새로 고치려면 마우스 오른쪽 단추 클릭). 목록 뷰 데이터가 내용 창에 표시됩니다.  
  
5.  데이터 계층 응용 프로그램의 목록 뷰를 보려면 **배포된 데이터 계층 응용 프로그램** 노드를 클릭합니다(새로 고치려면 마우스 오른쪽 단추 클릭). 목록 뷰 데이터가 내용 창에 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [배포된 데이터 계층 응용 프로그램 세부 정보&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)   
 [관리되는 인스턴스 세부 정보&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)   
 [유틸리티 관리&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)  
  
  

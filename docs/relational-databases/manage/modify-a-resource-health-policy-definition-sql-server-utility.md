---
title: 리소스 상태 정책 정의 수정(SQL Server 유틸리티) | Microsoft 문서
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
f1_keywords:
- sql13.SWB.UE.UTILITY.ADMINISTRATION.F1
ms.assetid: 27bec0b6-92e9-448e-8c70-fe36802cf128
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 65106ce68705f630b3955865b6967cfde0aae9a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32943398"
---
# <a name="modify-a-resource-health-policy-definition-sql-server-utility"></a>리소스 상태 정책 정의 수정(SQL Server 유틸리티)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 리소스 상태 정책 정의를 수정하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 리소스 사용률 정책을 수정하려면 먼저 UCP(유틸리티 제어 지점)를 만들어야 합니다. 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 리소스 사용률 정책은 데이터 계층 응용 프로그램 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스에 대해 구성할 수 있습니다. 리소스 사용률 정책은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 모든 데이터 계층 응용 프로그램 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에 대해 전역으로 정의하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 각 데이터 계층 응용 프로그램 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스에 대해 개별적으로 정의할 수 있습니다. 전역 정책을 구현하고 개별 데이터 계층 응용 프로그램 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스가 자체 정책 정의를 구성하도록 할 수도 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="modify-global-resource-utilization-policies-in-a-sql-server-utility"></a>SQL Server 유틸리티에서 전역 리소스 사용률 정책 수정  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 UCP에 연결합니다.  
  
2.  유틸리티 탐색기 탐색 창에서 **유틸리티 관리** 를 클릭하여 전역 모니터링 정책을 보거나 수정한 다음 유틸리티 탐색기 내용 창에서 **정책** 탭을 클릭합니다.  
  
3.  유틸리티 탐색기 내용 창에서 화살표나 정책 설명을 클릭하여 **전역 데이터 계층 모니터링 정책 설정** 또는 **전역 관리되는 인스턴스 모니터링 정책 설정** 을 선택합니다.  
  
4.  정책 설명 오른쪽에 있는 컨트롤을 사용하여 미달 사용 또는 초과 사용 정책 임계값을 설정합니다.  
  
5.  필요에 따라 **적용**, **삭제**또는 **기본값 복원** 단추를 사용합니다. 정책 변경이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 대시보드와 목록 뷰 세부 정보에 전파되고 표시되려면 최대 15분이 걸립니다.  
  
6.  데이터를 새로 고치려면 유틸리티 탐색기 탐색 창에서 **유틸리티 관리** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  
  
#### <a name="modify-resource-health-policy-definitions-for-an-individual-data-tier-application-or-an-individual-managed-instance-of-sql-server-in-a-sql-server-utility"></a>SQL Server 유틸리티에서 개별 데이터 계층 응용 프로그램 또는 개별 SQL Server 관리되는 인스턴스의 리소스 상태 정책 정의 수정  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 UCP에 연결합니다.  
  
2.  유틸리티 탐색기의 탐색 창에서 **배포된 데이터 계층 응용 프로그램**을 클릭하거나 **관리되는 인스턴스**를 클릭하여 개별 데이터 계층 응용 프로그램 또는 관리되는 인스턴스의 모니터링 정책을 보거나 수정합니다.  
  
3.  유틸리티 탐색기 내용 창 목록 뷰에서 수정하려는 정책이 있는 데이터 계층 응용 프로그램 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 클릭한 다음 **정책 정보** 탭을 클릭합니다.  
  
4.  화살표나 정책 설명을 클릭하여 보거나 수정하려는 정책을 선택합니다. 전역 정책이 기본적으로 선택됩니다.  
  
5.  전역 정책을 무시하고 지정된 데이터 계층 응용 프로그램의 개별 정책 정의를 구현하려면 라디오 단추를 **전역 정책 재정의** 로 선택합니다.  
  
6.  정책 설명 오른쪽에 있는 컨트롤을 사용하여 미달 사용 또는 초과 사용 정책 임계값을 설정합니다.  
  
7.  필요에 따라 **적용**, **삭제**또는 **기본값 복원** 단추를 사용합니다. 정책 변경이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 대시보드와 목록 뷰 세부 정보에 전파되고 표시되려면 최대 15분이 걸립니다.  
  
8.  데이터를 새로 고치려면 유틸리티 탐색기 탐색 창에서 **배포된 데이터 계층 응용 프로그램** 노드를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [리소스 상태 정책 결과 보기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)  
  
  

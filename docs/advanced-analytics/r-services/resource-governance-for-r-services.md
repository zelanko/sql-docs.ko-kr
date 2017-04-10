---
title: "R 서비스에 대 한 리소스 관리 | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# R 서비스에 대 한 리소스 관리
  R과 하나의 고민은 추가 하드웨어가 필요 다량의 프로덕션 환경에서 데이터를 분석 하 고 컴퓨터에 의해 제어 되지으로 데이터베이스 외부의 데이터를 자주 이동 IT 합니다.  고급 분석 작업을 수행 하려면 고객 데이터를 보호 하 고 데이터베이스 서버 리소스를 활용 하 여, 이러한 작업 보안 및 성능 등의 엔터프라이즈 수준의 규정 준수 요구 사항을 충족 하는 것이 필요할 수 있습니다.  
  
 이 섹션에서는 사용 하 여 실행 하는 R 작업 및 R 런타임에서 사용 하는 리소스를 관리 하는 방법에 대 한 정보를 제공 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 컨텍스트로 인스턴스.  
  
## 리소스 관리는 무엇입니까?  
 리소스 관리는 식별 하 고 여기서는 종종 여러 종속 응용 프로그램 및 여러 서비스를 지원 하 고 균형을 유지 하기 위해 데이터베이스 서버 환경에서 일반적으로 발생 된 문제를 방지 하도록 설계 되었습니다. 에 대 한 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 리소스 관리 이러한 작업을 수행 해야 합니다.  
  
-   서버 리소스가 너무 많이 사용 하는 스크립트를 식별 합니다.  
  
     관리자를 종료 하거나 너무 많은 리소스를 소모 하는 작업을 제한 해야 합니다.  
  
-   예측할 수 없는 작업을 완화 합니다.  
  
     예를 들어 여러 R 작업은 서버에서 동시에 실행 중인 경우 리소스 풀을 사용 하 여 작업을 서로 분리 되지 않습니다 인 한 리소스 충돌이 예기치 않은 성능이 정도 작업의 완료를 위협 합니다.  
  
-   작업 우선 순위를 지정 합니다.  
  
     관리자 또는 설계자 수, 우선 또는 리소스 충돌이 발생할 경우 완료 하는 특정 작업을 보장 해야 하는 작업을 지정할 수 있어야 합니다.  
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 를 사용할 수 있습니다 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) 원격 R 작업 및 R 런타임에서 사용 하는 리소스를 관리할 수 있습니다.  
  
## R 관리 작업을 사용 하 여 리소스 관리자를 표시 하는 방법  
 만들어서 R 작업에 할당 된 리소스를 관리 하는 일반적으로 *외부 리소스 풀* 풀 또는 풀에 작업을 할당 합니다. 외부 리소스 풀은 리소스 풀에 도입 된 새로운 유형의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], R 런타임 및 외부 데이터베이스 엔진에 다른 프로세스를 관리할 수 있도록 합니다.  
  
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 세 가지 유형의 기본 리소스 풀 됩니다.  
  
-    *내부 풀* 리소스 자체 SQL Server에서 사용 하 고 없습니다 변경 하거나 제한할 수를 나타냅니다.  
  
-    *풀 기본* 전체적으로 서버에 대 한 리소스 사용을 수정 하는 데 사용할 수 있는 미리 정의 된 사용자 풀입니다. 또한 리소스에 대 한 액세스를 관리 하려면이 풀에 속하는 사용자 그룹을 정의할 수 있습니다.  
  
-    *외부 풀 기본* 외부 리소스에 대 한 미리 정의 된 사용자 풀입니다. 또한 새 외부 리소스 풀을 만들 수 있으며이 풀에 속하는 사용자 그룹을 정의.  
  
 또한 만들 수 있습니다 *사용자 정의 리소스 풀* 데이터베이스 엔진 또는 다른 응용 프로그램에 리소스 할당을 만들려면 *외부 사용자 정의 리소스 풀* R 및 기타 외부 프로세스를 관리할 수 있습니다.  
  
 일반적인 개념 및 용어를 하는 데 유용한 정보를 참조 하십시오. [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)합니다.  
  
> [!NOTE]  
>  새 리소스 관리자 속성 DDL 문 또는; 스크립팅을 통해만 사용할 수 있는 현재 사용자 인터페이스를 사용 하 여 외부 리소스 그룹을 만들 수 없습니다 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다.  
  
## 리소스 관리자를 사용 하 여 리소스 관리 

   리소스 관리자를 처음 이라면 인스턴스 기본 리소스를 수정 하 고 새 외부 리소스 풀을 만들고 하는 방법의 간략 한 설명이이 항목을 참조 하십시오:  [How To: R에 대 한 리소스 풀 만들기](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 사용할 수는 *외부 리소스 풀* 다음 R 실행 파일에서 사용 하는 리소스를 관리 하는 메커니즘.  
  
-   Rterm.exe 및 위성 프로세스  
  
-   BxlServer.exe 및 위성 프로세스  
  
-   실행 패드를 통해 시작 하는 위성 프로세스  
  
 그러나 리소스 관리자를 사용 하 여 실행 패드 서비스에 대 한 직접 관리 지원 되지 않습니다. 있기 때문입니다는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 설계상 수 있는 신뢰할 수 있는 서비스를 Microsoft에서 제공 되는 시작 관리자만 호스트 됩니다. 신뢰할 수 있는 아이콘도 과도 한 리소스를 사용 하지 않도록 구성 됩니다.  
  
 리소스 관리자를 사용 하 여 위성 프로세스 관리는 개별 데이터베이스 구성 및 작업의 요구에 맞게 조정 하는 것이 좋습니다.  예를 들어, 모든 개별 위성 프로세스를 만들거나 실행 하는 동안 필요에 따라 삭제 합니다.  
  
## 외부 스크립트 실행을 사용 하지 않도록 설정  
 외부 스크립트에 대 한 지원은 선택 사항에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 합니다. 설치한 후에 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], 외부 스크립트를 실행 하는 기능은 기본적으로 꺼져 및 수동으로 속성을 다시 구성 하 고 스크립트 실행을 사용 하도록 인스턴스를 다시 시작 해야 합니다.  
  
 따라서 즉시 완화 해야 하는 리소스 문제 또는 보안 문제가 있는 경우 관리자가 즉시 해제할 수 모든 외부 스크립트 실행 사용 하 여 [sp_configure (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 속성을 설정 하 고 `external scripts enabled` FALSE 또는 0입니다.  
  
## 참고 항목  
 [R 솔루션 관리 및 모니터링](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [방법: R에 대 한 리소스 풀 만들기](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  
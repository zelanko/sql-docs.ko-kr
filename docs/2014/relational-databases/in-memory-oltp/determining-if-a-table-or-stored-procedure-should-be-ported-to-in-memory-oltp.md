---
title: 메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd81f459f09b06e0be06d53658b98b929eff5d6e
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395995"
---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]의 트랜잭션 성능 수집기를 사용하면 메모리 내 OLTP로 데이터베이스 응용 프로그램의 성능이 향상될지 평가할 수 있습니다. 트랜잭션 성능 분석 보고서에는 응용 프로그램에서 메모리 내 OLTP를 사용하기 위해 얼마나 많은 작업을 수행해야 하는지도 나와 있습니다. 메모리 내 OLTP에 이식할 디스크 기반 테이블을 식별한 후 [메모리 최적화 관리자](memory-optimization-advisor.md)를 사용하여 테이블을 마이그레이션할 수 있습니다. 마찬가지로 [Native Compilation Advisor](native-compilation-advisor.md) 를 사용하여 저장 프로시저를 고유하게 컴파일된 저장 프로시저에 이식할 수 있습니다.  
  
 이 항목에서는 다음과 같은 작업을 수행하는 방법에 대해 설명합니다.  
  
-   관리 데이터 웨어하우스 구성  
  
-   데이터 컬렉션 구성  
  
-   트랜잭션 성능 분석 보고서를 생성하여 성능이 중요한 테이블 및 저장 프로시저를 확인하십시오.  
  
 마이그레이션 방법에 대한 자세한 내용은 [메모리 내 OLTP – 일반적인 작업 패턴 및 마이그레이션 고려 사항](http://msdn.microsoft.com/library/dn673538.aspx)을 참조하세요.  
  
 트랜잭션 성능 수집기 및 트랜잭션 성능 분석 보고서를 사용하여 다음과 같은 작업을 수행할 수 있습니다.  
  
-   작업을 분석하여 메모리 내 OLTP로 성능이 향상될지를 확인합니다. 트랜잭션 성능 수집기는 작업의 성능 특징을 수집하고 평가합니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 그런 다음 트랜잭션 성능 분석 보고서는 메모리 내 OLTP로 변환할 경우 가장 이익이 되는 테이블과 저장 프로시저를 추천합니다.  
  
-   메모리 내 OLTP로 마이그레이션하는 작업을 계획하고 실행하는 데 도움이 됩니다. 디스크 기반 테이블에서 메모리 최적화 테이블로의 마이그레이션 경로는 시간이 많이 걸릴 수 있습니다. 메모리 최적화 관리자를 사용하여 테이블을 메모리 내 OLTP로 이동하기 전에 테이블에서 제거해야 하는 비호환성을 식별할 수 있습니다. 메모리 최적화 관리자는 메모리 액세스에 최적화된 테이블로의 테이블 마이그레이션이 응용 프로그램에 미치는 영향을 이해하는 데도 도움이 됩니다.  
  
     메모리 내 OLTP로 마이그레이션을 계획할 때와 일부 테이블과 저장 프로시저를 메모리 내 OLTP로 마이그레이션하려고 작업할 때마다 메모리 내 OLTP가 응용 프로그램에 도움이 되는지를 확인할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  데이터베이스 시스템의 성능은 다양한 요소에 따라 달라지며 트랜잭션 성능 수집기 중 일부는 관찰하고 측정하지 못할 수도 있습니다. 따라서 트랜잭션 성능 분석 보고서는 실제 성능 향상 정도가 어떠한 예측과도 일치한다고 보증하지 않습니다.  
  
 트랜잭션 성능 수집기와 트랜잭션 성능 분석 보고서를 생성 하는 기능을 선택 하면 설치 된 **관리 도구-기본** 하거나 **관리 도구-고급** 설치 하는 경우 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]합니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 다음 순서도에서는 권장 워크플로를 보여 줍니다. 노란색 노드는 선택적 절차를 나타냅니다.  
  
 ![AMR 워크플로](../../database-engine/media/amr-1.gif "AMR 워크플로")  
  
 성능 카운터 로그나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 작업 모니터를 사용하는 등의 다양한 방법으로 성능 기준을 설정할 수 있습니다. 성능 기준과 비교에 사용되는 정보는 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 CPU 사용량  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 메모리 사용량  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 I/O 작업  
  
-   트랜잭션을 처리하는 동안 인스턴스의 트랜잭션 처리량  
  
 트랜잭션 성능 수집기는 15분마다 데이터를 캡처합니다. 유용한 결과를 얻으려면 적어도 1시간 동안 트랜잭션 성능 수집기를 실행하십시오. 최상의 결과를 얻으려면 기본 시나리오의 데이터를 캡처하는 데 필요한 만큼 오래 트랜잭션 성능 수집기를 실행하십시오. 반드시 데이터 수집을 완료한 후에 트랜잭션 성능 분석 보고서를 생성하십시오.  
  
 최소한의 오버헤드를 위해 프로덕션 환경에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 실행하고 개발(테스트) 환경에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 데이터를 수집하도록 트랜잭션 성능 수집기를 구성하십시오. 원격 관리 데이터 웨어하우스 데이터베이스에서 데이터를 저장 하는 방법에 대 한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 참조 하십시오 [원격 SQL Server 인스턴스에서 데이터 컬렉션 구성](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md#xxx)합니다.  
  
## <a name="performance-impacts"></a>성능에 미치는 영향  
 트랜잭션 성능 수집기는 다음과 같은 두 개의 데이터 컬렉션 집합으로 구성됩니다.  
  
-   테이블 사용 분석  
  
-   저장 프로시저 분석  
  
 이 컬렉션 집합에서는 15분마다 3개의 DMV(동적 관리 뷰)에서 데이터를 수집하여 관리 데이터 웨어하우스로 작동하도록 구성된 데이터베이스로 데이터를 업로드합니다. 수집된 데이터를 업로드하면 성능에 최소의 영향을 미칩니다.  
  
## <a name="use-the-transaction-performance-collector"></a>트랜잭션 성능 수집기 사용  
 다음 단계를 수행하려면 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]의 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]이 필요합니다.  
  
> [!IMPORTANT]  
>  프로파일링 동안 스키마를 변경(데이터베이스 추가 또는 제거, 테이블 만들기 또는 삭제)하지 않습니다. 데이터를 수집하는 동안 데이터베이스 스키마를 변경하면 데이터베이스가 정확하게 보고서에 포함되지 않을 수 있습니다.  
  
### <a name="configure-management-data-warehouse"></a>관리 데이터 웨어하우스 구성  
 트랜잭션 성능 수집기를 사용하도록 관리 데이터 웨어하우스를 구성해야 합니다.  
  
 프로필 데이터를 수집할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 버전은 관리 데이터 웨어하우스가 구성되어 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 같은 버전이거나 이전 버전이어야 합니다.  
  
1.  개체 탐색기에서 **관리**를 확장합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **데이터 컬렉션** 선택한 **태스크** 차례로 **관리 데이터 웨어하우스 구성**합니다. 합니다 **관리 데이터 웨어하우스 구성 마법사** 시작 합니다.  
  
3.  클릭 **다음** 관리 데이터 웨어하우스 역할을 할 데이터베이스를 선택 합니다.  
  
4.  클릭 **새로 만들기** 프로필 데이터를 저장할 새 데이터베이스를 만들려고 합니다. 데이터베이스 만들기를 마친 후 클릭 **다음** 마법사에서.  
  
5.  마법사의 다음 단계에서 사용자와 로그인을 추가할 수 있습니다. 로그인을 MDW 인스턴스에 대한 역할 멤버 자격에 매핑할 수도 있습니다. 이 역할 멤버 자격은 로컬 인스턴스에서 데이터를 수집하는 데 필요하지 않습니다. 로컬 인스턴스에서 데이터를 수집하지 않는 경우 프로파일링할 트랜잭션을 실행할 계정에 데이터베이스 역할 멤버 자격 `mdw_admin`을 부여해도 됩니다. 마치면 클릭 **다음**합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트가 실행 중인지 확인합니다.  
  
7.  다음 화면에서 클릭 **완료** 마법사를 종료 합니다.  
  
### <a name="configure-data-collection-on-a-local-includessnoversionincludesssnoversion-mdmd-instance"></a>로컬 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 데이터 컬렉션 구성  
 데이터 컬렉션을 사용하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 시작해야 합니다. 데이터 수집기는 서버에 하나만 구성하면 됩니다.  
  
 SQL Server 2012 또는 이후 버전의 데이터 수집기를 구성할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
 같은 인스턴스에서 관리 데이터 웨어하우스 데이터베이스로 업로드하기 위해 데이터 컬렉션을 구성하려면  
  
1.  **개체 탐색기**를 확장 하 고 **관리**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **데이터 컬렉션**를 선택 **태스크**, 차례로 **데이터 컬렉션 구성**합니다. 합니다 **데이터 컬렉션 구성 마법사** 시작 합니다.  
  
3.  클릭 **다음** 프로필 데이터를 수집 하는 데이터베이스를 선택 합니다.  
  
4.  현재 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 선택하고 이 서버 인스턴스에서 관리 데이터 웨어하우스 데이터베이스를 선택합니다.  
  
5.  입력란에 **사용 하도록 설정 하려는 데이터 수집기 집합 선택**를 선택 **트랜잭션 성능 컬렉션 집합**합니다. 클릭 **다음** 완료 합니다.  
  
6.  선택 내용을 확인합니다. 클릭 **다시** 설정을 수정 합니다. 완료되었으면 **마침** 을 클릭합니다.  
  
###  <a name="xxx"></a> 원격 데이터 컬렉션 구성 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스  
 데이터를 수집하려면 데이터를 수집하는 인스턴스에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 시작해야 합니다.  
  
 SQL Server 2012 또는 이후 버전의 데이터 수집기를 구성할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
 트랜잭션이 프로파일링된 인스턴스와 다른 인스턴스에 있는 관리 데이터 웨어하우스 데이터베이스에 데이터를 업로드하려면 데이터 수집기에 대한 올바른 자격 증명으로 설정된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 프록시가 필요합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 프록시를 사용하도록 설정하려면 먼저 도메인이 활성화된 로그인을 사용하여 자격 증명을 설정해야 합니다. 도메인이 활성화된 로그인은 관리 데이터 웨어하우스 데이터베이스에 대한 `mdw_admin` 그룹의 멤버여야 합니다. 참조 [방법: 자격 증명 (SQL Server Management Studio) 만들기](http://msdn.microsoft.com/library/ms190703\(v=sql.105\).aspx) 자격 증명을 만드는 방법에 대 한 정보에 대 한 합니다.  
  
 다른 인스턴스에서 관리 데이터 웨어하우스 데이터베이스로 업로드하기 위해 데이터 컬렉션을 구성하려면  
  
1.  메모리 내 OLTP로 마이그레이션하려는 디스크 기반 개체가 포함 된 인스턴스를 확장 합니다 **관리** 개체 탐색기에서 노드.  
  
2.  마우스 오른쪽 단추로 클릭 **데이터 컬렉션** 선택한 **태스크** 차례로 **데이터 컬렉션 구성**합니다. 합니다 **데이터 컬렉션 구성 마법사** 시작 합니다.  
  
3.  클릭 **다음** 프로필 데이터를 수집 하는 데이터베이스를 선택 합니다.  
  
4.  관리 데이터 웨어하우스 데이터베이스가 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 있는지 확인합니다.  
  
5.  다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 선택하고 이 인스턴스에서 관리 데이터 웨어하우스 데이터베이스를 선택합니다.  
  
     프로필 데이터를 수집할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 버전은 관리 데이터 웨어하우스가 구성되어 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 같은 버전이거나 이전 버전이어야 합니다.  
  
6.  입력란에 **사용 하도록 설정 하려는 데이터 수집기 집합 선택**를 선택 **트랜잭션 성능 컬렉션 집합**합니다.  
  
7.  선택 **사용을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 원격 업로드를 위해 에이전트 프록시**합니다.  
  
8.  클릭 **다음** 완료 합니다.  
  
9. 프록시를 선택합니다.  
  
     새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 프록시를 만들려는 경우  
  
    1.  클릭 **새로 만들기** 표시할 합니다 **새 프록시 계정** 대화 상자.  
  
    2.  에 **새 프록시 계정** 대화 상자에서 프록시 이름을 입력 자격 증명을 선택 하 고 필요에 따라 설명을 입력 합니다. 그런 다음 클릭 **주체**합니다.  
  
    3.  클릭 **추가** 선택한 **Msdb** 역할입니다.  
  
    4.  선택 `dc_proxy` 누릅니다 **확인**합니다. 누른 **확인** 다시 합니다.  
  
     올바른 프록시를 선택한 후 클릭 **다음**합니다.  
  
10. 시스템 컬렉션 집합을 구성 하려면 다음을 확인 **시스템 컬렉션 집합** 누릅니다 **다음**합니다.  
  
11. 선택 내용을 확인합니다. 클릭 **다시** 설정을 수정 합니다. 끝나면 **완료** 완료 합니다.  
  
 이제 인스턴스에서 데이터 컬렉션 집합이 구성되어 실행됩니다.  
  
### <a name="generate-reports"></a>보고서 생성  
 관리 데이터 웨어하우스의 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 트랜잭션 성능 분석 보고서를 생성할 수 있습니다 **보고서**, 한 다음 **관리 데이터 웨어하우스**, 차례로 **트랜잭션 성능 분석 개요**합니다.  
  
 보고서는 작업 서버에서 모든 사용자 데이터베이스에 대한 정보를 수집합니다. MDW(관리 데이터 웨어하우스) 데이터베이스가 로컬 컴퓨터에 있는 경우 MDW 데이터베이스가 보고서에 나타납니다.  
  
 CPU 시간 대 경과 시간 비율이 높은 저장 프로시저는 마이그레이션 대상으로 적합합니다. 고유하게 컴파일된 저장 프로시저는 메모리 최적화 테이블을 참조만 할 수 있기 때문에 보고서에 모든 테이블 참조가 표시되므로 마이그레이션 비용이 추가될 수 있습니다.  
  
 테이블에 대한 세부 정보 보고서는 다음 세 개의 섹션으로 구성됩니다.  
  
-   검색 통계 섹션  
  
     이 섹션에는 데이터베이스 테이블에 대한 검색에 대해 수집된 통계를 보여 주는 단일 테이블이 있습니다. 열은 다음과 같습니다.  
  
    -   총 액세스의 백분율. 전체 데이터베이스의 작업과 관련되어 이 테이블에서 수행된 검색에 대한 백분율입니다. 이 백분율이 높을수록 데이터베이스의 다른 테이블과 비교하여 해당 테이블이 더 많이 사용된 것입니다.  
  
    -   조회 통계/범위 검색 통계. 이 열은 프로파일링 동안 테이블에 대해 수행된 포인트 조회 및 범위 검색(인덱스 검색 및 테이블 검색) 수를 기록합니다. 트랜잭션당 평균이 예상치입니다.  
  
    -   Interop 게인 및 네이티브 게인. 이러한 열을 통해 테이블이 메모리 최적화 테이블로 변환된 경우 포인트 조회 또는 범위 검색으로 얻을 수 있는 성능 이점을 예상할 수 있습니다.  
  
-   경합 통계 섹션  
  
     이 섹션에는 데이터베이스 테이블에 대한 경합을 보여 주는 테이블이 있습니다. 데이터베이스 래치 및 잠금에 대 한 자세한 내용은 참조 하십시오 [잠금 아키텍처](http://msdn.microsoft.com/library/aa224738\(v=sql.80\).aspx)합니다. 열은 다음과 같습니다.  
  
    -   총 대기의 백분율. 데이터베이스 작업과 비교하여 이 데이터베이스 테이블에 대한 래치 및 잠금 대기에 대한 백분율입니다. 이 백분율이 높을수록 데이터베이스의 다른 테이블과 비교하여 해당 테이블이 더 많이 사용된 것입니다.  
  
    -   래치 통계. 이러한 열은 이 테이블의 관련 쿼리에 대한 래치 대기 수를 기록합니다. 래치에 대 한 내용은 참조 하세요 [래칭](http://msdn.microsoft.com/library/aa224727\(v=SQL.80\).aspx)합니다. 이 숫자가 클수록 테이블에 대한 래치 경합이 더 큰 것입니다.  
  
    -   잠금 통계. 이 열 그룹은 이 테이블에 대한 페이지 잠금 획득 및 쿼리 대기 수를 기록합니다. 잠금에 대 한 자세한 내용은 참조 하세요. [SQL Server의 잠금 이해](http://msdn.microsoft.com/library/aa213039\(v=SQL.80\).aspx)합니다. 대기가 많을수록 테이블에 대한 잠금 경합이 더 큰 것입니다.  
  
-   마이그레이션 문제 섹션  
  
     이 섹션에는 이 데이터베이스 테이블을 메모리 최적화 테이블로 변환할 때 발생한 문제를 보여 주는 테이블이 있습니다. 문제 등급이 높을수록 테이블 변환에 문제가 많은 것입니다. 이 데이터베이스 테이블을 변환 하려면 세부 정보를 보려면 사용 하십시오 합니다 [메모리 최적화 관리자](memory-optimization-advisor.md)합니다.  
  
 테이블 세부 정보 보고서에 대 한 검색 및 경합 통계는 수집 되 고에서 집계 [sys.dm_db_index_operational_stats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql)합니다.  
  
 저장 프로시저에 대한 세부 정보 보고서는 다음 두 개의 섹션으로 구성됩니다.  
  
-   실행 통계 섹션  
  
     이 섹션에는 저장 프로시저 실행에 대해 수집된 통계를 보여 주는 테이블이 있습니다. 열은 다음과 같습니다.  
  
    -   캐시된 시간. 이 실행 계획이 캐시된 시간입니다. 저장 프로시저가 계획 캐시에서 삭제되고 다시 입력될 때 각 캐시에 대한 시간이 발생합니다.  
  
    -   총 CPU 시간. 프로파일링 동안 저장 프로시저에서 사용한 총 CPU 시간입니다. 이 숫자가 클수록 저장 프로시저에서 CPU를 더 많이 사용한 것입니다.  
  
    -   총 실행 시간. 프로파일링 동안 저장 프로시저에서 사용한 총 실행 시간입니다. 이 숫자와 CPU 시간 간의 차이가 클수록 저장 프로시저에서 비효율적으로 CPU를 사용하는 것입니다.  
  
    -   누락된 총 캐시. 프로파일링 동안 저장 프로시저 실행으로 인해 발생한 캐시 누락(실제 저장소에서 읽기) 수입니다.  
  
    -   실행 수. 프로파일링 동안 이 저장 프로시저가 실행한 횟수입니다.  
  
-   테이블 참조 섹션  
  
     이 섹션에는 이 저장 프로시저가 참조하는 테이블을 보여 주는 테이블이 있습니다. 저장 프로시저를 고유하게 컴파일된 저장 프로시저로 변환하기 전에 이러한 모든 테이블은 메모리 최적화 테이블로 변환되어야 하며 동일한 서버 및 데이터베이스에 있어야 합니다.  
  
 저장된 프로시저 세부 정보 보고서에 대 한 실행 통계 수집 및 집계에서 되 [sys.dm_exec_procedure_stats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql)합니다. 참조에서 가져온 [sys.sql_expression_dependencies &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)합니다.  
  
 저장된 프로시저를 고유 하 게 컴파일된 저장 프로시저로 변환 하는 방법에 대 한 세부 정보를 보려면 사용 하십시오 합니다 [네이티브 컴파일 관리자](native-compilation-advisor.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)  
  
  

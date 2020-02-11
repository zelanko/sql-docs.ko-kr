---
title: 테스트 서버 사용 시 고려 사항 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- overhead [Database Engine Tuning Advisor]
- tuning overhead [SQL Server]
- reducing production server tuning load
- Database Engine Tuning Advisor [SQL Server], test servers
- xp_msver
- test servers [Database Engine Tuning Advisor]
- production servers [SQL Server]
- offload tuning overhead [SQL Server]
ms.assetid: 94e6c3e5-1f09-4616-9da2-4e44d066d494
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c1ed99e6ee3ef6385e6041044e9b2cb829b1b3ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63151138"
---
# <a name="considerations-for-using-test-servers"></a>테스트 서버 사용 시 고려 사항
  테스트 서버를 사용하여 프로덕션 서버의 데이터베이스를 튜닝하는 것은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자의 중요한 장점입니다. 이 기능을 사용하여 프로덕션 서버의 실제 데이터를 테스트 서버로 복사하지 않고도 튜닝 오버헤드를 테스트 서버에 오프로드할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자 GUI(그래픽 사용자 인터페이스)에서는 테스트 서버 튜닝 기능이 지원되지 않습니다.  
  
 이 기능을 성공적으로 사용하려면 다음 섹션에 나열된 고려 사항을 검토하십시오.  
  
## <a name="setting-up-the-test-serverproduction-server-environment"></a>테스트 서버/프로덕션 서버 환경 설정  
  
-   테스트 서버를 사용하여 프로덕션 서버의 데이터베이스를 튜닝하려는 사용자는 두 서버 모두에 존재해야 합니다. 그렇지 않으면 이 시나리오를 실행할 수 없습니다.  
  
-   확장 저장 프로시저인 **xp_msver**는 테스트 서버/프로덕션 서버 시나리오를 사용하도록 설정해야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 이 확장 저장 프로시저를 사용하여 테스트 서버를 튜닝하는 동안 사용할 프로세서 수와 프로덕션 서버의 사용 가능한 메모리를 인출합니다. **xp_msver** 을 사용할 수 없는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자를 실행하는 컴퓨터의 하드웨어 특징을 가정합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자를 실행하는 컴퓨터의 하드웨어 특징을 알 수 없는 경우 프로세서는 하나이고 메모리는 1024MB라고 가정합니다. 이 확장 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치될 때 기본적으로 튜닝됩니다. 자세한 내용은 [노출 영역 구성](../security/surface-area-configuration.md) 및 [xp_msver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/xp-msver-transact-sql)를 참조하세요.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 테스트 서버와 프로덕션 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전이 같다고 가정합니다. 버전이 서로 다른 경우 테스트 서버의 버전이 우선 적용됩니다. 예를 들어 테스트 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard를 실행하는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 프로덕션 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise를 실행하고 있어도 인덱싱된 뷰, 분할 및 온라인 작업을 권장 구성에 포함하지 않습니다.  
  
## <a name="about-test-serverproduction-server-behavior"></a>테스트 서버/프로덕션 서버 동작 정보  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 권장 구성을 만들 때 프로덕션 서버와 테스트 서버 간의 하드웨어 차이를 고려합니다. 권장 구성은 튜닝이 프로덕션 서버에서만 수행된 경우와 동일합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 튜닝에 필요한 통계 작성뿐만 아니라 메타데이터 수집을 위해 프로덕션 서버에 일부 로드를 설정할 수 있습니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 실제로 데이터를 프로덕션 서버에서 테스트 서버로 복사하지 않고 데이터베이스의 메타데이터와 필요한 통계만을 복사합니다.  
  
-   모든 세션 정보는 프로덕션 서버의 **msdb** 에 저장됩니다. 따라서 튜닝에 사용할 수 있는 모든 테스트 서버를 이용할 수 있으며 모든 세션에 대한 정보를 한 곳(프로덕션 서버)에서 확인할 수 있습니다.  
  
## <a name="issues-related-to-the-shell-database"></a>셸 데이터베이스와 관련된 문제점  
  
-   튜닝 작업 후 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 튜닝 프로세스 중에 테스트 서버에서 만든 모든 메타데이터를 제거해야 합니다. 여기에는 셸 데이터베이스도 포함됩니다. 동일한 프로덕션 서버와 테스트 서버에서 일련의 튜닝 세션을 수행하고 있는 경우 시간을 절약하기 위해 이 셸 데이터베이스를 계속 유지할 수 있습니다. XML 입력 파일의 **TuningOptions** 상위 요소 아래에서 **RetainShellDB** 하위 요소와 다른 하위 요소를 지정합니다. 이러한 옵션을 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자가 셸 데이터베이스를 유지합니다. 자세한 내용은 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](database-engine-tuning-advisor.md)를 참조하세요.  
  
-   **RetainShellDB** 하위 요소를 지정하지 않은 경우에도 성공적으로 수행한 테스트 서버/프로덕션 서버 튜닝 세션 후에 셸 데이터베이스가 테스트 서버에 남아 있을 수 있습니다. 필요 없는 이러한 셸 데이터베이스는 후속 튜닝 세션을 방해할 수 있으므로 다른 테스트 서버/프로덕션 서버 튜닝 세션을 수행하기 전에 삭제해야 합니다. 또한 튜닝 세션이 예기치 않게 종료되면 테스트 서버의 셸 데이터베이스와 해당 데이터베이스 내의 개체가 테스트 서버에 남아 있을 수 있습니다. 새 테스트 서버/프로덕션 서버 튜닝 세션을 시작하기 전에 이러한 데이터베이스와 개체를 삭제해야 합니다.  
  
## <a name="issues-related-to-the-tuning-process"></a>튜닝 프로세스와 관련된 문제점  
  
-   사용자는 프로덕션 서버와 테스트 서버 간의 차이로 인해 발생하는 튜닝 오류와 메타데이터를 프로덕션 서버에서 테스트 서버로 복사할 때 발생하는 오류의 튜닝 로그를 확인해야 합니다. 예를 들어 사용자 로그인은 테스트 서버에 존재하지 않을 수도 있습니다. 사용자 로그인이 테스트 서버에 존재하지 않는 경우 해당 사용자 로그인에 의해 발생한 작업의 이벤트는 튜닝할 수 없습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자 GUI를 사용하여 튜닝 로그를 볼 수 있습니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자가 테스트 서버에서 만든 셸 데이터베이스에 개체가 없어서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에서 많은 이벤트를 튜닝할 수 없는 경우 튜닝 로그를 확인해야 합니다. 튜닝할 수 없는 이벤트는 로그에 나열됩니다. 테스트 서버에서 데이터베이스를 성공적으로 튜닝하려면 사용자가 셸 데이터베이스에서 누락된 개체를 만든 다음 새 튜닝 세션을 시작해야 합니다.  
  
-   같은 이름을 가진 데이터베이스가 테스트 서버에 있는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 메타데이터를 복사하지는 않지만 튜닝 작업을 계속하고 필요한 통계를 수집합니다. 이 기능은 사용자가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자를 호출하기 전에 이미 테스트 서버에 데이터베이스를 만들고 해당 메타데이터를 복사한 경우에 유용합니다.  
  
-   프로덕션 서버의 데이터베이스에 대해 DATE_CORRELATION_OPTIMIZATION 옵션이 설정되어 있는 경우 이 옵션과 연관된 메타데이터와 데이터는 테스트 서버를 튜닝하는 동안 완전히 스크립팅되지 않습니다. 테스트 서버/프로덕션 서버 시나리오에 대해 튜닝을 수행할 때 다음과 같은 문제가 적용될 수 있습니다.  
  
    -   사용자는 DATE_CORRELATION_OPTIMIZATION 옵션을 사용하는 쿼리를 위해 서버에 여러 쿼리 계획을 가질 수 있습니다.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 권장 구성 스크립트에서 DATE_CORRELATION_OPTIMIZATION 옵션을 강제 적용하는 인덱싱된 뷰의 삭제를 제안할 수 있습니다.  
  
     그러므로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자가 해당 비용은 알지만 이점을 모르기 때문에 상관 관계 통계를 포함하는 인덱싱된 뷰에 대해 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에서 제안한 권장 구성은 무시할 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 DATE_CORRELATION_OPTIMIZATION을 설정한 경우에 유용한 **datetime** 열의 클러스터형 인덱스와 같은 특정 인덱스의 선택을 권장하지 않을 수 있습니다.  
  
     뷰가 상관 관계 통계 기반인지 여부를 확인하려면 **sys.views** 카탈로그 뷰의 [is_date_correlation_view](/sql/relational-databases/system-catalog-views/sys-views-transact-sql) 열을 선택합니다.  
  
  

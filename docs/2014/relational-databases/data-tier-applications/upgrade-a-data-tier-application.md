---
title: 데이터 계층 애플리케이션 업그레이드 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.upgradedacwizard.reviewpolicy.f1
- sql12.swb.upgradedacwizard.selectoptions.f1
- sql12.swb.upgradedacwizard.selectpackage.f1
- sql12.swb.upgradedacwizard.reviewplan.f1
- sql12.swb.upgradedacwizard.checkdrift.f1
- sql12.swb.upgradedacwizard.summary.f1
- sql12.swb.upgradedacwizard.upgradedac.f1
- sql12.swb.upgradedacwizard.introduction.f1
helpviewer_keywords:
- upgrade DAC
- data-tier application [SQL Server], upgrade
- wizard [DAC], upgrade
- How to [DAC], upgrade
ms.assetid: c117df94-f02b-403f-9383-ec5b3ac3763c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 44c4bb7c01f18db6062ad1982fcf5a5f80e4d6b0
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797983"
---
# <a name="upgrade-a-data-tier-application"></a>데이터 계층 애플리케이션 업그레이드
  데이터 계층 애플리케이션 업그레이드 마법사 또는 Windows PowerShell 스크립트를 사용하여 현재 배포된 DAC(데이터 계층 애플리케이션)의 스키마와 속성을 새 DAC 버전에 정의된 스키마와 속성과 일치하도록 변경할 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [DAC 업그레이드 옵션 선택](#ChoseDACUpgOptions), [제한 사항](#LimitationsRestrictions), [필수 구성 요소](#Prerequisites), [보안](#Security), [사용 권한](#Permissions)  
  
-   **DAC를 업그레이드하려면:** [데이터 계층 애플리케이션 업그레이드 마법사](#UsingDACUpgradeWizard), [PowerShell](#UpgradeDACPowerShell)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 DAC 업그레이드는 기존 데이터베이스의 스키마를 새 DAC 버전에 정의된 스키마와 일치하도록 변경하는 전체 업그레이드 프로세스입니다. 새 버전의 DTS가 DAC 패키지 파일에 제공됩니다. DAC 패키지를 만드는 방법은 [데이터 계층 애플리케이션](data-tier-applications.md)을 참조하세요.  
  
###  <a name="ChoseDACUpgOptions"></a> DAC 업그레이드 옵션 선택  
 전체 업그레이드에는 4가지 업그레이드 옵션이 있습니다.  
  
-   **데이터 손실 무시** -`True`경우 일부 작업으로 인해 데이터가 손실 되더라도 업그레이드가 진행 됩니다. `False`인 경우 이러한 작업은 업그레이드를 종료합니다. 예를 들어, 현재 데이터베이스의 테이블이 새로운 DAC의 스키마에 제공되지 않는 경우 `True`가 지정되면 테이블이 삭제됩니다. 기본 설정은 `True`입니다.  
  
-   **변경 시 차단** -`True`경우 데이터베이스 스키마가 이전 DAC에 정의 된 스키마와 다르면 업그레이드가 종료 됩니다. `False`인 경우 변경이 감지되어도 업그레이드가 계속됩니다. 기본 설정은 `False`입니다.  
  
-   **오류 발생 시 롤백** -`True`경우 업그레이드가 트랜잭션에 포함 되 고 오류가 발생 하면 롤백이 시도 됩니다. `False`인 경우 변경이 되면 모든 변경 내용이 커밋되고 오류가 발생하면 데이터베이스의 이전 백업을 복원해야 할 수 있습니다. 기본 설정은 `False`입니다.  
  
-   **정책 유효성 검사 건너뛰기** -`True`경우 DAC 서버 선택 정책이 평가 되지 않습니다. `False`인 경우 정책이 평가되고 유효성 검사 오류가 있으면 업그레이드가 종료됩니다. 기본 설정은 `False`입니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 DAC 업그레이드는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4(서비스 팩 4) 이상에서만 수행될 수 있습니다.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 업그레이드를 시작하기 전에 전체 데이터베이스 백업을 수행하는 것이 좋습니다. 업그레이드할 때 오류가 발생하여 모든 변경 내용을 롤백할 수 없는 경우 백업을 복원해야 할 수 있습니다.  
  
 업그레이드를 시작하기 전에 DAC 패키지 및 업그레이드 동작의 유효성을 검사하기 위해 취해야 하는 조치는 여러 가지가 있습니다. 이러한 검사를 수행하는 방법은 [Validate a DAC Package](validate-a-dac-package.md)를 참조하세요.  
  
-   출처를 알 수 없거나 신뢰할 수 없는 DAC 패키지를 사용하여 업그레이드하지 않는 것이 좋습니다. 이러한 패키지에 포함된 악성 코드가 의도하지 않은 Transact-SQL 코드를 실행하거나 스키마를 수정하여 오류가 발생할 수 있습니다. 출처를 알 수 없거나 신뢰할 수 없는 패키지를 사용하려면 먼저 DAC의 압축을 풀고 저장 프로시저나 다른 사용자 정의 코드와 같은 코드를 검사하세요.  
  
-   마지막 버전의 DAC가 배포된 후 현재 데이터베이스가 변경된 경우 일부 변경 사항으로 인해 업그레이드가 성공적으로 완료되지 못하거나 업그레이드에 의해 일부 변경 사항이 제거될 수 있습니다. 먼저 데이터베이스의 변경 내용에 대한 보고서를 생성하고 검토해야 합니다.  
  
-   업그레이드가 수행할 스키마 변경 목록을 생성하고 목록에서 문제가 있는지 검토하는 것이 좋습니다.  
  
 DAC 패키지의 애플리케이션 이름이 현재 배포된 DAC의 애플리케이션 이름과 일치해야 합니다. 예를 들어 현재 DAC의 애플리케이션 이름이 **GeneralLedger**이면 마찬가지로 애플리케이션 이름이 **GeneralLedger**인 DAC 패키지를 사용해야 업그레이드할 수 있습니다.  
  
 모든 수정 사항을 기록할 수 있는 충분한 트랜잭션 로그 공간이 있는지 확인합니다.  
  
###  <a name="Security"></a> 보안  
 보안을 개선하기 위해 SQL Server 인증 로그인은 암호 없이 DAC 패키지에 저장됩니다. 패키지가 배포 또는 업그레이드되면 생성된 암호와 함께 비활성 로그인이 생성됩니다. 로그인을 활성화하려면 ALTER ANY LOGIN 권한이 있는 로그인을 사용하여 로그인하고 ALTER LOGIN을 사용하여 로그인을 활성화하여 사용자에게 알려 줄 수 있는 새 암호를 할당합니다. Windows 인증 로그인의 경우 암호가 SQL Server에서 관리되지 않으므로 이 과정이 필요 없습니다.  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버를 통하거나 **dbcreator** 고정 서버 역할에 포함되고 ALTER ANY LOGIN 권한이 있는 로그인을 통해서만 DAC를 업그레이드할 수 있습니다. 로그인은 기존 데이터베이스의 소유자여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sa **라는 기본 제공** 시스템 관리자 계정도 DAC를 업그레이드할 수 있습니다.  
  
##  <a name="UsingDACUpgradeWizard"></a> 데이터 계층 애플리케이션 업그레이드 마법사 사용  
 **마법사를 사용하여 DAC를 업그레이드하려면**  
  
1.  **개체 탐색기**에서 업그레이드할 DAC가 포함된 인스턴스에 대한 노드를 확장합니다.  
  
2.  **관리** 노드, **데이터 계층 애플리케이션** 노드를 차례로 확장합니다.  
  
3.  업그레이드할 DAC에 대한 노드를 마우스 오른쪽 단추로 클릭한 다음, **데이터 계층 애플리케이션 업그레이드...** 를 선택합니다.  
  
4.  마법사 대화 상자를 완료합니다.  
  
    1.  [소개 페이지](#Introduction)  
  
    2.  [패키지 선택 페이지](#Select_dac_package)  
  
    3.  [정책 검토 페이지](#Review_policy)  
  
    4.  [변경 내용 검색 페이지](#Detect_change)  
  
    5.  [업그레이드 계획 검토](#ReviewUpgPlan)  
  
    6.  [요약 페이지](#Summary)  
  
    7.  [DAC 업그레이드 페이지](#Upgrade)  
  
##  <a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 데이터 계층 애플리케이션을 업그레이드하는 단계에 대해 설명합니다.  
  
 **이 페이지를 다시 표시 안 함** - 앞으로 이 페이지가 표시되지 않도록 하려면 이 확인란을 클릭합니다.  
  
 **다음 >** - **패키지 선택** 페이지로 진행합니다.  
  
 **취소** - DAC를 업그레이드하지 않고 마법사를 종료합니다.  
  
##  <a name="Select_dac_package"></a> 패키지 선택 페이지  
 이 페이지를 사용하여 데이터 계층 애플리케이션의 새 버전을 포함하는 DAC 패키지를 지정할 수 있습니다. 이 페이지는 두 가지 상태로 전환됩니다.  
  
### <a name="select-the-dac-package"></a>DAC 패키지 선택  
 이 페이지의 초기 상태를 사용하여 배포할 DAC 패키지를 선택할 수 있습니다. DAC 패키지는 유효한 DAC 패키지 파일이어야 하며 확장자가 .dacpac여야 합니다. DAC 패키지의 DAC 애플리케이션 이름이 현재 DAC의 애플리케이션 이름과 같아야 합니다.  
  
 **DAC 패키지** - 새 버전의 데이터 계층 애플리케이션이 포함된 DAC 패키지의 경로와 파일 이름을 지정합니다. 입력란 오른쪽의 **찾아보기** 단추를 선택하여 DAC 패키지의 위치를 찾아볼 수 있습니다.  
  
 **애플리케이션 이름** - DAC를 만들거나 데이터베이스에서 추출할 때 할당된 DAC 애플리케이션 이름을 표시하는 읽기 전용 입력란입니다.  
  
 **버전** - DAC를 만들거나 데이터베이스에서 추출할 때 할당된 버전을 표시하는 읽기 전용 입력란입니다.  
  
 **설명** - DAC를 만들거나 데이터베이스에서 추출할 때 작성된 설명을 표시하는 읽기 전용 입력란입니다.  
  
 **\< 이전** - **소개** 페이지로 진행합니다.  
  
 **다음 >** - 선택한 파일이 유효한 DAC 패키지인지 마법사에서 확인하는 동안 진행률 표시줄이 표시됩니다.  
  
 **취소** - DAC를 업그레이드하지 않고 마법사를 종료합니다.  
  
### <a name="validating-the-dac-package"></a>DAC 패키지 유효성 검사  
 선택한 파일이 유효한 DAC 패키지인지 마법사에서 확인하는 동안 진행률 표시줄이 표시됩니다. DAC 패키지의 유효성이 확인되면 마법사는 **정책 검토** 페이지로 진행합니다. 파일이 유효한 DAC 패키지가 아닌 경우 마법사는 **DAC 패키지 선택** 페이지에서 유지됩니다. 이 경우 다른 유효한 DAC 패키지를 선택하거나 마법사를 취소하고 새 DAC 패키지를 생성할 수 있습니다.  
  
 **DAC 내용의 유효성을 검사하고 있습니다** - 유효성 검사의 현재 상태를 보고하는 진행률 표시줄입니다.  
  
 **\< 이전** - **패키지 선택** 페이지의 초기 상태로 돌아갑니다.  
  
 **다음 >** - **패키지 선택** 페이지의 최종 버전으로 진행합니다.  
  
 **취소** - DAC를 배포하지 않고 마법사를 종료합니다.  
  
##  <a name="Review_policy"></a> 정책 검토 페이지  
 DAC에 정책이 있는 경우 이 페이지를 사용하여 DAC 서버 선택 정책을 평가한 결과를 검토할 수 있습니다. DAC 서버 선택 정책은 선택적이며 Microsoft Visual Studio에서 DAC를 작성하면 여기에 할당됩니다. 정책에서는 서버 선택 정책 패싯을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 DAC를 호스팅하기 위해 충족해야 하는 조건을 지정합니다.  
  
 **정책 조건의 평가 결과** - DAC 서버 선택 정책의 조건에 대한 평가가 성공했는지 보여 주는 읽기 전용 보고서입니다. 각 조건을 평가한 결과가 별도의 행에 보고됩니다.  
  
 **정책 위반을 무시합니다.** - 정책 조건이 한 개 이상 실패하더라도 배포를 진행하려면 이 확인란을 사용합니다. 실패한 모든 조건이 DAC 작동에 영향을 주지 않는 것이 확실한 경우에만 이 옵션을 선택합니다.  
  
 **\< 이전** - **패키지 선택** 페이지로 돌아갑니다.  
  
 **다음 >** - **변경 내용 검색** 페이지로 진행합니다.  
  
 **취소** - DAC를 업그레이드하지 않고 마법사를 종료합니다.  
  
##  <a name="Detect_change"></a> 변경 내용 검색 페이지  
 이 페이지를 사용하여 **msdb**의 DAC 메타데이터에 저장된 스키마 정의와 스키마가 다른 데이터베이스 변경 내용에 대해 마법사가 확인한 결과를 보고할 수 있습니다. 예를 들어 DAC를 배포한 후에 CREATE, ALTER 또는 DROP 문을 사용하여 데이터베이스에 개체를 추가, 변경 또는 제거했을 수 있습니다. 페이지에 먼저 진행률 표시줄이 표시된 다음 보고서의 분석 결과가 표시됩니다.  
  
 **변경 내용을 검색하고 있습니다. 몇 분 정도 걸릴 수 있습니다.** - 마법사가 데이터베이스의 현재 스키마와 DAC 정의의 개체 간의 차이를 분석하는 동안 진행률 표시줄을 표시합니다.  
  
 **변경 내용 검색 결과:** - 분석이 완료되었음을 나타내고 아래에 결과를 보고합니다.  
  
 **데이터베이스 DatabaseName이 변경되지 않았습니다.** - 마법사가 데이터베이스에 정의된 개체와 DAC 정의의 해당 항목 간에 차이를 검색하지 못했습니다.  
  
 **데이터베이스 DatabaseName이 변경되었습니다.** - 마법사가 데이터베이스에 정의된 개체와 DAC 정의의 해당 항목 간에 차이를 검색했습니다.  
  
 **변경 내용이 손실되더라도 계속합니다.** - 현재 데이터베이스의 개체나 데이터 일부가 새 데이터베이스에 누락될 수 있음을 이해하고 업그레이드를 계속하도록 지정합니다. 변경 내용 보고서를 분석했으며 새 데이터베이스에 필요한 개체나 데이터를 수동으로 전송하는 데 필요한 단계를 이해하는 경우에만 이 단추를 사용해야 합니다. 확실하지 않은 경우에는 **보고서 저장** 단추를 클릭하여 보고서를 저장하고 **취소**를 클릭합니다. 보고서를 분석하고 업그레이드 완료 후에 필요한 개체와 데이터를 전송하는 방법을 계획한 다음 마법사를 다시 시작합니다.  
  
 **보고서 저장** - 마법사가 데이터베이스의 개체와 DAC 정의의 해당 항목 간에 검색한 변경 내용에 대한 보고서를 저장하려면 단추를 클릭합니다. 그런 다음 보고서를 검토하여 업그레이드 완료 후에 보고서에 나열된 개체 일부나 전부를 새 데이터베이스에 통합하기 위한 동작을 수행해야 하는지 결정할 수 있습니다.  
  
 **\< 이전** - **DAC 패키지 선택** 페이지로 돌아갑니다.  
  
 **다음 >** - **옵션** 페이지로 진행합니다.  
  
 **취소** - DAC를 배포하지 않고 마법사를 종료합니다.  
  
## <a name="options-page"></a>옵션 페이지  
 이 페이지를 사용하여 업그레이드에 대한 실패 시 롤백 옵션을 선택합니다.  
  
 **오류 발생 시 롤백** - 오류가 발생할 경우에 마법사에서 롤백을 시도할 수 있는 트랜잭션에 업그레이드를 포함하려면 이 옵션을 선택합니다. 이 옵션에 대한 자세한 내용은 [DAC 업그레이드 옵션 선택](#ChoseDACUpgOptions)을 참조하세요.  
  
 **기본값 복원** - 기본 설정인 false로 옵션을 반환합니다.  
  
 **\< 이전** - **변경 내용 검색** 페이지로 돌아갑니다.  
  
 **다음>** - **업그레이드 계획 검토** 페이지로 진행합니다.  
  
 **취소** - DAC를 배포하지 않고 마법사를 종료합니다.  
  
##  <a name="ReviewUpgPlan"></a> 업그레이드 계획 검토 페이지  
 이 페이지를 사용하여 업그레이드 프로세스에서 수행할 동작을 검토합니다. 업그레이드가 문제를 만들지 않을 거라고 확신하는 경우에만 계속합니다.  
  
 **DAC를 업그레이드하는 데 사용되는 동작은 다음과 같습니다.** - 표시된 정보를 검토하여 수행할 동작이 올바른지 확인합니다. **동작** 열에서는 Transact-SQL 문과 같은 동작을 표시하고 업그레이드를 수행하기 위해 실행됩니다. 연결된 동작으로 인해 데이터가 삭제될 수 있는 경우 **데이터 손실** 열에 경고가 표시됩니다.  
  
 **새로 고침** – 동작 목록을 새로 고칩니다.  
  
 **동작 보고서 저장** – 동작 창의 콘텐츠를 HTML 파일로 저장합니다.  
  
 **변경 내용이 손실되더라도 계속합니다.** - 현재 데이터베이스의 개체나 데이터 일부가 새 데이터베이스에 누락될 수 있음을 이해하고 업그레이드를 계속하도록 지정합니다. 변경 내용 보고서를 분석했으며 새 데이터베이스에 필요한 개체나 데이터를 수동으로 전송하는 데 필요한 단계를 이해하는 경우에만 이 단추를 사용해야 합니다. 확실하지 않은 경우에는 **동작 보고서 저장** 단추를 클릭하여 변경 보고서를 저장하고 **스크립트 저장** 단추로 Transact-SQL 스크립트를 저장한 다음 **취소**를 클릭합니다. 보고서와 스크립트를 분석하고 업그레이드를 완료하고 마법사를 다시 시작한 이후에 필요한 개체와 데이터를 전송하는 방법을 계획합니다.  
  
 **스크립트 저장** - 텍스트 파일로 업그레이드를 수행하는 데 사용될 Transact-SQL 문을 저장합니다.  
  
 **기본값 복원** - 기본 설정인 false로 옵션을 반환합니다.  
  
 **\< 이전** - **변경 내용 검색** 페이지로 돌아갑니다.  
  
 **다음 >** - **요약** 페이지로 진행합니다.  
  
 **취소** - DAC를 배포하지 않고 마법사를 종료합니다.  
  
##  <a name="Summary"></a> 요약 페이지  
 이 페이지에서는 DAC를 업그레이드할 때 마법사에서 수행할 동작을 최종적으로 검토할 수 있습니다.  
  
 **DAC를 업그레이드하는 데 사용되는 설정은 다음과 같습니다.** - 표시된 정보를 검토하여 수행할 동작이 올바른지 확인합니다. 창에는 업그레이드하도록 선택한 DAC, 새 버전의 DAC를 포함하는 DAC 패키지가 표시됩니다. 창에는 데이터베이스의 현재 버전이 현재 DAC 정의와 동일한지 또는 데이터베이스가 변경되었는지도 표시됩니다.  
  
 **\< 이전** - **업그레이드 계획 검토** 페이지로 돌아갑니다.  
  
 **다음 >** - DAC를 배포하고 **DAC 업그레이드** 페이지에 결과를 표시합니다.  
  
 **취소** - DAC를 배포하지 않고 마법사를 종료합니다.  
  
##  <a name="Upgrade"></a> DAC 업그레이드 페이지  
 이 페이지에서는 업그레이드 작업의 성공 또는 실패를 보고합니다.  
  
 **DAC를 업그레이드하고 있습니다.** - DAC를 업그레이드하기 위해 수행한 각 동작의 성공 또는 실패를 보고합니다. 정보를 검토하여 각 동작의 성공 또는 실패를 확인합니다. 오류가 발생한 동작에는 모두 **결과** 열에 링크가 있습니다. 링크를 선택하면 해당 동작의 오류에 대한 보고서가 표시됩니다.  
  
 **보고서 저장** - 업그레이드 보고서를 HTML 파일로 저장하려면 이 단추를 선택합니다. 파일은 모든 동작에서 생성된 모든 오류를 비롯하여 각 동작의 상태를 보고합니다. 기본 폴더는 Windows 계정의 Documents 폴더 아래의 SQL Server Management Studio\DAC Packages 폴더입니다.  
  
 **마침** - 마법사를 종료합니다.  
  
##  <a name="UpgradeDACPowerShell"></a> PowerShell 사용  
 **PowerShell 스크립트에서 IncrementalUpgrade() 메서드를 사용하여 DAC를 업그레이드하려면**  
  
1.  SMO Server 개체를 만든 다음 업그레이드할 DAC를 포함하는 인스턴스로 설정합니다.  
  
2.  `ServerConnection` 개체를 열고 동일한 인스턴스에 연결합니다.  
  
3.  `System.IO.File`을 사용하여 DAC 패키지 파일을 로드합니다.  
  
4.  `add_DacActionStarted` 및 `add_DacActionFinished`를 사용하여 DAC 업그레이드 이벤트에 등록합니다.  
  
5.  `DacUpgradeOptions`를 설정합니다.  
  
6.  `IncrementalUpgrade` 메서드를 사용하여 DAC를 업그레이드합니다.  
  
7.  DAC 패키지 파일을 읽는 데 사용되는 파일 스트림을 닫습니다.  
  
### <a name="example-powershell"></a>예제(PowerShell)  
 다음 예에서는 MyApplicationVNext.dacpac 패키지의 새 DAC 버전을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 기본 인스턴스에서 MyApplicaiton이라는 DAC를 업그레이드합니다.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplicationVNext.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC upgrade events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Upgrade the DAC and close the package.  
$dacName  = "MyApplication"  
  
## Set the upgrade options.  
$upgradeProperties = New-Object Microsoft.SqlServer.Management.Dac.DacUpgradeOptions  
$upgradeProperties.blockonchanges = $true  
$upgradeProperties.ignoredataloss = $false  
$upgradeProperties.rollbackonfailure = $true  
$ upgradeProperties.skippolicyvalidation = $false  
  
## Upgrade the DAC  
$dacstore.IncrementalUpgrade($dacName, $dacType, $upgradeProperties)  
## Close the package file.  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>관련 항목:  
 [개체 탐색기](data-tier-applications.md)   
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  

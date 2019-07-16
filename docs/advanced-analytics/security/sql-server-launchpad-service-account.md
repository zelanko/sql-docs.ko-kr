---
title: SQL Server 실행 패드 서비스 계정 구성-SQL Server Machine Learning 서비스
description: SQL Server에 대 한 외부 스크립트 실행에 사용 되는 SQL Server 실행 패드 서비스 계정을 수정 하는 방법.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: ad6377e73633d34b322e5f455f0dd08143c53529
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962332"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server 실행 패드 서비스 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 관리 하 고 전체 텍스트 인덱싱 및 쿼리 서비스가 전체 텍스트 쿼리를 처리 하는 것에 대 한 별도 호스트를 실행 하는 방식과 유사 하 게 외부 스크립트를 실행 하는 서비스입니다.

자세한 내용은 실행 패드 섹션을 참조 [SQL Server Machine Learning Services의 확장성 아키텍처](../../advanced-analytics/concepts/extensibility-framework.md#launchpad) 고 [SQL Server Machine Learning의 확장성 프레임 워크에 대 한 보안 개요 서비스](../../advanced-analytics/concepts/security.md#launchpad)합니다.

## <a name="account-permissions"></a>계정 권한

기본적으로 SQL Server 실행 패드에서 실행 되도록 구성 됩니다 **NT Service\MSSQLLaunchpad**, 외부 스크립트를 실행 하는 데 필요한 모든 권한으로 프로 비전 된입니다. 이 계정에서 권한을 제거 실패을 시작 하거나 외부 스크립트를 실행 해야 하는 SQL Server 인스턴스에 액세스 하는 실행 패드에서 발생할 수 있습니다.

서비스 계정, 수정 하는 경우 사용 해야 합니다 [로컬 보안 정책 콘솔](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)합니다.

이 계정에 필요한 사용 권한에 다음 표에 나열 됩니다.

| 그룹 정책 설정 | 상수 이름 |
|----------------------|---------------|
| [프로세스의 메모리 할당량 조정](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [트래버스 검사 무시](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [서비스로 로그온](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [프로세스 수준 토큰 바꾸기](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

SQL Server 서비스를 실행하는 데 필요한 권한에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>구성 속성

일반적으로 서비스 구성을 수정할 수 없는 이유는. 속성 변경 될 수 있는 서비스 계정을 포함, 외부 프로세스 (기본적으로 20) 또는 암호의 수에는 작업자 계정에 대 한 정책을 다시 설정 합니다.

1. [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 엽니다.

2. SQL Server 서비스에서 SQL Server 실행 패드를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.
  + 서비스 계정을 변경 하려면 클릭 합니다 **로그온** 탭 합니다.
  + 사용자 수를 늘리려면 클릭 합니다 **고급** 탭을 변경 합니다 **보안 컨텍스트 수**합니다.

> [!Note]
> SQL Server 2016 R Services의 초기 버전에서는 서비스의 일부 속성을 편집 하 여 변경할 수 있습니다는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 구성 파일입니다. 이 파일은 구성 변경에 대 한 더 이상 사용 됩니다. SQL Server 구성 관리자는 서비스 계정 및 사용자 수와 같은 서비스 구성 변경에 대 한 올바른 접근 방법입니다.

## <a name="debug-settings"></a>디버그 설정

만 디버깅 등 제한 된 경우에 유용할 수 있는 실행 패드의 구성 파일을 사용 하 여 몇 가지 속성을 변경할 수 있습니다. 구성 파일 중에 생성 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 하 고 기본적으로에 일반 텍스트 파일로 저장 됩니다 `<instance path>\binn\rlauncher.config`합니다.

이 파일을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 중인 컴퓨터의 관리자여야 합니다. 파일을 편집하는 경우 변경 내용을 저장하기 전에 백업 복사본을 만드는 것이 좋습니다.

다음 표에서 대 한 고급 설정을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 허용 되는 값입니다.

|**설정 이름**|**형식**|**설명**|
|----|----|----|
|작업\_정리\_ON\_종료|정수 |이 내부 설정-이 값을 변경 하지 마십시오. </br></br>세션이 완료 된 후 각 외부 런타임 세션에 대해 생성 된 임시 작업 폴더를 정리할 해야 여부를 지정 합니다. 이 설정은 디버깅 작업에 유용합니다. </br></br>지원 되는 값은 **0** (해제) 또는 **1** (사용). </br></br>기본값은 1, 종료 시 의미 로그 파일이 제거 됩니다.|
|추적\_수준|정수 |디버깅을 위해 MSSQLLAUNCHPAD 추적의 자세한 정도 수준을 구성 합니다. 이 LOG_DIRECTORY 설정에 의해 지정 된 경로에서 추적 파일을 영향을 줍니다. </br></br>지원되는 값은 다음과 같습니다. **1** (오류), **2** (성능)에 **3** (경고), **4** (정보). </br></br>기본값은 1, 출력 오류만을 의미 합니다.|

모든 설정은 별도 줄의 각 설정으로 키-값 쌍의 형식을 사용합니다. 예를 들어, 추적 수준을 변경 하는 줄 추가 `Default: TRACE_LEVEL=4`합니다.

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>암호 정책 강제 적용

암호를 주기적으로 변경해야 하는 정책이 조직에 있는 경우에는 실행 패드 서비스를 통해 실행 패드에서 작업자 계정용으로 유지 관리하는 암호화된 암호를 강제로 다시 생성해야 할 수 있습니다.

이 설정을 사용하도록 설정하고 암호를 강제로 새로 고치려면 SQL Server 구성 관리자에서 실행 패드 서비스에 대한 **속성** 창을 열고, **고급**을 클릭하고, **외부 사용자 암호 다시 설정**을 **예**로 변경합니다. 이 변경을 적용하면 모든 사용자 계정의 암호가 즉시 다시 생성됩니다. 이 변경 후 외부 스크립트를 실행 될 때 새로 생성 된 암호를 읽게 할 실행 패드 서비스를 다시 시작 해야 합니다.

암호를 주기적으로 다시 설정하려면 이 플래그를 수동으로 설정하거나 스크립트를 사용합니다.

## <a name="next-steps"></a>다음 단계

+ [확장성 프레임 워크](../concepts/extensibility-framework.md)
+ [보안 개요](../concepts/security.md)

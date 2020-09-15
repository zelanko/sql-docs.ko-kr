---
title: 실행 패드 계정 구성
description: SQL Server에서 외부 스크립트 실행에 사용되는 SQL Server 실행 패드 서비스 계정을 수정하는 방법입니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/17/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 38b00fd3a5f300a4038c6c302c1311a2f135d97b
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180408"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server 실행 패드 서비스 구성
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]는 전체 텍스트 인덱싱 및 쿼리 서비스에서 전체 텍스트 쿼리를 처리하기 위해 별도의 호스트를 시작하는 것과 비슷한 방식으로 외부 스크립트를 관리하고 실행하는 서비스입니다.

자세한 내용은 [SQL Server Machine Learning Services의 확장성 아키텍처](../../machine-learning/concepts/extensibility-framework.md#launchpad) 및 [SQL Server Machine Learning Services의 확장성 프레임워크에 대한 보안 개요](../../machine-learning/concepts/security.md#launchpad)의 실행 패드 섹션을 참조하세요.

## <a name="account-permissions"></a>계정 권한

기본적으로 SQL Server 실행 패드는 외부 스크립트 실행을 위한 모든 필수 권한이 프로비저닝되어 있는 **NT Service\MSSQLLaunchpad** 아래에서 실행되도록 구성되어 있습니다. 이 계정에서 권한을 제거하면 실행 패드 시작 또는 외부 스크립트를 실행해야 하는 SQL Server 인스턴스 액세스가 실패할 수 있습니다.

서비스 계정을 수정할 경우 [로컬 보안 정책 콘솔](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)을 사용해야 합니다.

이 계정에 필요한 권한은 다음 표에 나열되어 있습니다.

| 그룹 정책 설정 | 상수 이름 |
|----------------------|---------------|
| [프로세스에 대한 메모리 할당량 조정](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [트래버스 검사 바이패스](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [서비스로 로그온](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [프로세스 수준의 토큰 대체](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

SQL Server 서비스를 실행하는 데 필요한 권한에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>구성 속성

일반적으로 서비스 구성은 수정할 이유가 없습니다. 변경 가능한 속성에는 서비스 계정, 외부 프로세스 수(기본적으로 20) 또는 작업자 계정에 대한 암호 재설정 정책이 포함됩니다.

1. [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 엽니다.

2. SQL Server Services 아래에서 SQL Server 실행 패드를 마우스 오른쪽 버튼으로 클릭하고 **속성**을 선택합니다.
  + 서비스 계정을 변경하려면 **로그온** 탭을 클릭합니다.
  + 사용자 수를 늘리려면 **고급** 탭을 클릭하고 **보안 컨텍스트 수**를 변경합니다.

> [!Note]
> 초기 버전의 SQL Server 2016 R Services에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 구성 파일을 편집하여 서비스의 일부 속성을 변경할 수 있었습니다. 이 파일은 더 이상 구성 변경을 위해 사용되지 않습니다. 서비스 계정 및 사용자 수와 같은 서비스 구성을 변경하기 위해서는 SQL Server 구성 관리자를 사용해야 합니다.

## <a name="debug-settings"></a>디버그 설정

몇 가지 속성은 실행 패드의 구성 파일을 사용해서만 변경할 수 있으며, 이는 디버깅과 같은 제한된 경우에 유용할 수 있습니다. 구성 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 생성되며, 기본적으로 일반 텍스트 파일로 `<instance path>\binn\rlauncher.config`에 저장됩니다.

이 파일을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 중인 컴퓨터의 관리자여야 합니다. 파일을 편집하는 경우 변경 내용을 저장하기 전에 백업 복사본을 만드는 것이 좋습니다.

다음 표에는 허용 값과 함께 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 고급 설정이 표시되어 있습니다.

|**설정 이름**|**형식**|**설명**|
|----|----|----|
|JOB\_CLEANUP\_ON\_EXIT|정수 |이 값은 내부 전용 설정입니다. 이 값을 변경하지 마십시오. </br></br>각 외부 런타임 세션에 대해 생성된 임시 작업 폴더를 세션이 완료된 후 정리해야 하는지 여부를 지정합니다. 이 설정은 디버깅 작업에 유용합니다. </br></br>지원되는 값은 **0**(사용 안 함) 또는 **1**(사용)입니다. </br></br>기본값은 종료 시 로그 파일이 제거됨을 나타내는 1입니다.|
|TRACE\_LEVEL|정수 |디버깅용으로 MSSQLLAUNCHPAD의 추적 세부 정보 표시 수준을 구성합니다. LOG_DIRECTORY 설정으로 지정된 경로의 추적 파일에 영향을 줍니다. </br></br>지원되는 값은 다음과 같습니다. **1**(오류), **2**(성능), **3**(경고), **4**(정보). </br></br>기본값은 출력 오류만 나타내는 1입니다.|

모든 설정은 별도 줄의 각 설정으로 키-값 쌍의 형식을 사용합니다. 예를 들어 추적 수준을 변경하려면 `Default: TRACE_LEVEL=4` 줄을 추가해야 합니다.

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>암호 정책 강제 적용

암호를 주기적으로 변경해야 하는 정책이 조직에 있는 경우에는 실행 패드 서비스를 통해 실행 패드에서 작업자 계정용으로 유지 관리하는 암호화된 암호를 강제로 다시 생성해야 할 수 있습니다.

이 설정을 사용하도록 설정하고 암호를 강제로 새로 고치려면 SQL Server 구성 관리자에서 실행 패드 서비스에 대한 **속성** 창을 열고, **고급**을 클릭하고, **외부 사용자 암호 다시 설정**을 **예**로 변경합니다. 이 변경을 적용하면 모든 사용자 계정의 암호가 즉시 다시 생성됩니다. 이 변경 후에 외부 스크립트를 실행하려면 실행 패드 서비스를 다시 시작해야 합니다. 이때 새로 생성된 암호를 읽습니다.

암호를 주기적으로 다시 설정하려면 이 플래그를 수동으로 설정하거나 스크립트를 사용합니다.

## <a name="next-steps"></a>다음 단계

+ [확장성 프레임워크](../concepts/extensibility-framework.md)
+ [보안 개요](../concepts/security.md)

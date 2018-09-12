---
title: SQL Server 실행 패드 서비스 계정 구성 | Microsoft Docs
description: SQL Server에 대 한 외부 스크립트 실행에 사용 되는 SQL Server 실행 패드 서비스 계정을 수정 하는 방법.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0afdb02c578de92bc91c5f47e973148136ebd919
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892911"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server 실행 패드 서비스 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

별도 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] SQL Server machine learning (R 또는 Python) 통합을 추가한 데이터베이스 엔진 인스턴스에 대 한 서비스가 만들어집니다.

## <a name="service-account-configuration"></a>서비스 계정 구성

기본적으로 SQL Server 실행 패드에서 실행 되도록 구성 됩니다 **NT Service\MSSQLLaunchpad**, 외부 스크립트를 실행 하는 데 필요한 모든 권한으로 프로 비전 된입니다. 이 계정에서 권한을 제거 실패을 시작 하거나 외부 스크립트를 실행 해야 하는 SQL Server 인스턴스에 액세스 하는 실행 패드에서 발생할 수 있습니다.

이 계정에 대 한 필요한 사용 권한 아래에 나열 됩니다. 서비스 계정, 수정 하는 경우 사용 해야 합니다 **로컬 보안 정책** 이러한 사용 권한을 포함 하도록 응용 프로그램:

+ 프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)
+ 트래버스 검사 무시(SeChangeNotifyPrivilege)
+ 서비스로 로그온(SeServiceLogonRight)
+ 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)

SQL Server 서비스를 실행하는 데 필요한 권한에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>구성 속성

1. [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 엽니다. 

2. SQL Server 실행 패드를 마우스 오른쪽 단추로 클릭 **속성**합니다.

    + 서비스 계정을 변경 하려면 클릭 합니다 **로그온** 탭 합니다.

    + 사용자의 수를 늘리려면 클릭 합니다 **고급** 탭 합니다.

> [!Note]
> SQL Server 2016 R Services의 초기 버전에서는 서비스의 일부 속성을 편집 하 여 변경할 수 있습니다는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 구성 파일입니다. 이 파일은 구성 변경에 대 한 더 이상 사용 됩니다. SQL Server 구성 관리자는 서비스 계정 및 사용자 수와 같은 서비스 구성 변경에 대 한 올바른 접근 방법입니다.

#### <a name="debug-settings"></a>디버그 설정

만 디버깅 등 제한 된 경우에 유용할 수 있는 실행 패드의 구성 파일을 사용 하 여 몇 가지 속성을 변경할 수 있습니다. 구성 파일 하는 동안 만들어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 하 고 기본적으로 다음 위치에서 일반 텍스트 파일로 저장 됩니다. `<instance path>\binn\rlauncher.config`

이 파일을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 중인 컴퓨터의 관리자여야 합니다. 파일을 편집하는 경우 변경 내용을 저장하기 전에 백업 복사본을 만드는 것이 좋습니다.

다음 표에서 대 한 고급 설정을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 허용 되는 값입니다. 

|**설정 이름**|**형식**|**설명**|
|----|----|----|
|작업\_정리\_ON\_종료|정수 |이 내부 설정 –이 값을 변경 하지 마십시오. </br></br>세션이 완료 된 후 각 외부 런타임 세션에 대해 생성 된 임시 작업 폴더를 정리할 해야 여부를 지정 합니다. 이 설정은 디버깅 작업에 유용합니다. </br></br>지원 되는 값은 **0** (해제) 또는 **1** (사용). </br></br>기본값은 1, 종료 시 의미 로그 파일이 제거 됩니다.|
|추적\_수준|정수 |디버깅을 위해 MSSQLLAUNCHPAD 추적의 자세한 정도 수준을 구성 합니다. 이 LOG_DIRECTORY 설정에 의해 지정 된 경로에서 추적 파일을 영향을 줍니다. </br></br>지원 되는 값: **1** (오류), **2** (성능)에 **3** (경고), **4** (정보). </br></br>기본값은 1, 출력 경고만 의미 합니다.|

모든 설정은 별도 줄의 각 설정으로 키-값 쌍의 형식을 사용합니다. 예를 들어, 추적 수준을 변경 하는 줄 추가 `Default: TRACE_LEVEL=4`합니다.

## <a name="see-also"></a>참고자료

[확장성 프레임 워크](../concepts/extensibility-framework.md)

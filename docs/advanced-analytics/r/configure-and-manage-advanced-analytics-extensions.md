---
title: SQL Server Machine Learning Services에 대 한 고급 구성 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8384773f6db4c0ced2fc68e52cd78100c98c52fd
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396364"
---
# <a name="advanced-configuration-options-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에 대 한 고급 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 외부 스크립트 런타임 및 SQL server에서 machine learning과 관련 된 기타 서비스의 구성을 수정 하려면 설치 후 만들 수 있는 변경 내용을 설명 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

##  <a name="bkmk_Provisioning"></a> 추가 사용자 프로 비전에 대 한 계정 기계 학습

외부 스크립트 처리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한이 낮은 로컬 사용자 계정의 컨텍스트에서 실행 됩니다. 개별 낮은 권한 계정에서 이러한 프로세스를 실행 중인 다음과 같은 이점이 있습니다.

+ 외부 스크립트 런타임 프로세스의 권한에서 감소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터
+ Python 또는 R 등의 외부 런타임의 세션 간에 격리를 제공합니다.

새 Windows 설치 프로그램의 일부로 *사용자 계정 풀* 만들어집니다 R 또는 Python 등의 외부 런타임 프로세스를 실행 하는 데 필요한 로컬 사용자 계정을 포함 하 합니다. 기계 학습 작업을 지 원하는 데 필요한 사용자 수를 수정할 수 있습니다. 

또한 데이터베이스 관리자는 기계 학습에 사용 되는 인스턴스에 연결 하려면이 그룹 사용 권한을 부여 해야 합니다. 자세한 내용은 [SQL Server Machine Learning Services에 대 한 사용자 계정 풀 수정](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

Protext 중요 한 리소스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],이 그룹에 대 한 액세스 제어 목록 (ACL)을 정의할 수 있습니다. 그룹에 대 한 액세스를 거부 된 리소스를 지정 하 여 R 또는 Python 런타임 같은 외부 프로세스에서 액세스를 방지할 수 있습니다.

+ 사용자 계정 풀은 특정 인스턴스에 연결됩니다. 컴퓨터에 학습에 사용 하도록 설정한 각 인스턴스에 대 한 별도 풀 작업자 계정에 필요 합니다. 인스턴스 간에 계정을 공유할 수 없습니다.

+ 풀의 사용자 계정 이름은 SQLInstanceName*nn*의 형식입니다. 예를 들어 기본 인스턴스 machine learning을 사용 하는 경우 사용자 계정 풀 MSSQLSERVER01, MSSQLSERVER02 등과 같은 계정 이름을 지원 합니다.

+ 사용자 계정 풀의 크기는 정적이고 기본값은 20입니다. 이 사용자 계정 풀의 크기에 따라 동시에 시작할 수 있는 외부 런타임 세션 수가 제한 됩니다. 이 제한을 변경 하려면 관리자로 SQL Server 구성 관리자를 사용 해야 합니다.

사용자 계정 풀을 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server Machine Learning Services에 대 한 사용자 계정 풀 수정](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

##  <a name="bkmk_ManagingMemory"></a> 외부 스크립트 프로세스에 사용 되는 메모리 관리

기본적으로 machine learning에 대 한 외부 스크립트 런타임을 개 이하의 총 컴퓨터 메모리의 20%로 제한 됩니다. 시스템에서 다르지만 일반적으로 볼 수 있습니다이 한도 모델을 학습 데이터 행 예측 등 심각한 기계 학습 작업에 대 한 부적절 한입니다. 

기계 학습을 지원 하려면 관리자로이 제한을 늘릴 수 있습니다. 이렇게 하면 예약 된 메모리의 양을 줄이기 위해 해야 할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 다른 서비스에 대 한 합니다. 또한 R 또는 Python 작업에 특정 리소스 풀을 할당할 수 있도록 외부 리소스 풀 또는 풀을 정의 하려면 리소스 관리자를 사용 하는 것이 좋습니다.

자세한 내용은 [machine learning 위한 리소스 거 버 넌 스](../../advanced-analytics/r/resource-governance-for-r-services.md)합니다.


## <a name="bkmk_Launchpad"></a>실행 패드 서비스 계정 수정

별도 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] machine learning 서비스를 구성한 각 인스턴스에 대 한 서비스가 만들어집니다.

기본적으로 실행 패드는 R 스크립트를 실행하는 데 필요한 모든 권한으로 프로비전된 NT Service\MSSQLLaunchpad 계정을 사용하여 실행되도록 구성됩니다. 그러나이 계정을 변경 하면 경우 실행 패드 못할를 시작 하거나 외부 스크립트를 실행 해야는 SQL Server 인스턴스에 액세스할 수 있습니다.

서비스 계정을 수정하는 경우 **로컬 보안 정책** 응용 프로그램을 사용하고 다음 사용 권한을 포함하도록 각 서비스 계정의 사용 권한을 업데이트해야 합니다.

+ 프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)
+ 트래버스 검사 무시(SeChangeNotifyPrivilege)
+ 서비스로 로그온(SeServiceLogonRight)
+ 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)

SQL Server 서비스를 실행하는 데 필요한 권한에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.

##  <a name="bkmk_ChangingConfig"></a> 고급 서비스 옵션 변경

SQL Server 2016 R Services의 초기 버전에서는 서비스의 일부 속성을 편집 하 여 변경할 수 있습니다는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 구성 파일입니다. 

그러나이 파일은 구성 변경에 대 한 더 이상 사용 됩니다. 서비스 계정 및 사용자 수와 같은 서비스 구성 변경 내용을 적용 하려면 SQL Server 구성 관리자를 사용 하는 것이 좋습니다.

**실행 패드 구성을 수정 하려면**

1. [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 엽니다. 
2. SQL Server 실행 패드를 마우스 오른쪽 단추로 클릭 **속성**합니다.

    + 서비스 계정을 변경 하려면 클릭 합니다 **로그온** 탭 합니다.

    + 사용자의 수를 늘리려면 클릭 합니다 **고급** 탭 합니다.


**디버그 설정을 수정 하려면**

만 디버깅 등 제한 된 경우에 유용할 수 있는 실행 패드의 구성 파일을 사용 하 여 몇 가지 속성을 변경할 수 있습니다. 구성 파일 하는 동안 만들어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 하 고 기본적으로 다음 위치에서 일반 텍스트 파일로 저장 됩니다. `<instance path>\binn\rlauncher.config`

이 파일을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 중인 컴퓨터의 관리자여야 합니다. 파일을 편집하는 경우 변경 내용을 저장하기 전에 백업 복사본을 만드는 것이 좋습니다.

다음 표에서 대 한 고급 설정을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 허용 되는 값입니다. 

|**설정 이름**|**형식**|**설명**|
|----|----|----|
|작업\_정리\_ON\_종료|정수 |이 내부 설정 –이 값을 변경 하지 마십시오. </br></br>세션이 완료 된 후 각 외부 런타임 세션에 대해 생성 된 임시 작업 폴더를 정리할 해야 여부를 지정 합니다. 이 설정은 디버깅 작업에 유용합니다. </br></br>지원 되는 값은 **0** (해제) 또는 **1** (사용). </br></br>기본값은 1, 종료 시 의미 로그 파일이 제거 됩니다.|
|추적\_수준|정수 |디버깅을 위해 MSSQLLAUNCHPAD 추적의 자세한 정도 수준을 구성 합니다. 이 LOG_DIRECTORY 설정에 의해 지정 된 경로에서 추적 파일을 영향을 줍니다. </br></br>지원 되는 값: **1** (오류), **2** (성능)에 **3** (경고), **4** (정보). </br></br>기본값은 1, 출력 경고만 의미 합니다.|

모든 설정은 별도 줄의 각 설정으로 키-값 쌍의 형식을 사용합니다. 예를 들어, 추적 수준을 변경 하는 줄 추가 `Default: TRACE_LEVEL=4`합니다.

## <a name="see-also"></a>관련 항목

[보안 고려 사항](security-considerations-for-the-r-runtime-in-sql-server.md)

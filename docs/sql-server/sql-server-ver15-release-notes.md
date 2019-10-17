---
title: SQL Server 2019 릴리스 정보 | Microsoft Docs
ms.date: 10/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 9b6895abfa0b09459911eba03b52837379f2d162
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041194"
---
# <a name="sql-server-2019-preview-release-notes"></a>SQL Server 2019 미리 보기 릴리스 정보
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]의 관련 제한 사항 및 알려진 문제에 대해 설명합니다. 관련 내용은 다음을 참조하세요.

>[SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md)

>[!NOTE]
>콘텐츠는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 릴리스 후보에 게시됩니다. 릴리스 후보는 시험판 소프트웨어입니다. 정보는 변경될 수 있습니다. 지원 시나리오에 대한 자세한 내용은 [지원](#support)을 참조하세요.

## <a name="includesql-server-2019includessssqlv15-mdmd-release-candidate-rc"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] RC(릴리스 후보)

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]의 최신 공개 릴리스입니다.

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC는 Evaluation Edition으로만 사용 가능합니다. 다른 에디션은 사용할 수 없습니다.

릴리스 후보 소프트웨어의 지원 및 라이선스에 관한 전체 세부 정보는 설치 미디어가 포함된 `license_Eval.rtf` 내에 있습니다.

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

## <a name="documentation"></a>설명서

- **문제 및 고객에게 미치는 영향**: SQL Server 2019(15.x)의 설명서는 제한되며 내용은 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 설명서 세트에 포함되어 있습니다. SQL Server 2019(15.x)와 관련된 문서의 내용은 **적용 대상**에서 설명합니다.

- **문제 및 고객에게 미치는 영향**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설명서는 버전별로 필터링할 수 있습니다. 각 설명서 페이지의 왼쪽 맨 위에 있는 컨트롤을 사용하여 요구 사항에 맞게 필터링합니다.

- **문제 및 고객에게 미치는 영향**: SQL Server 2019(15.x) 관련 오프라인 콘텐츠는 제공되지 않습니다.

## <a name="build-number"></a>빌드 번호

Windows, Linux 및 컨테이너에서 SQL Server 2019 RC의 빌드 번호는 `15.0.1900.25`입니다.  빅 데이터 클러스터에서 사용되는 SQL Server 2019 RC의 빌드 번호는 `15.0.1900.47`입니다.

## <a name="hardware-and-software-requirements"></a>하드웨어 및 소프트웨어 요구 사항

- **문제 및 고객에게 미치는 영향**: 하드웨어 및 소프트웨어 요구 사항은 계속 검토 중이며 제품 릴리스에 포함할 최종 내용이 아닙니다.

  - **하드웨어**
    - [Windows - 프로세서, 메모리 및 운영 체제 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - 시스템 요구 사항](../linux/sql-server-linux-setup.md#system)
  - **소프트웨어**
    - Windows Server 2016 이상. 추가 요구 사항은 [SQL Server 설치 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.
    - Microsoft .NET Framework 4.6.2. [다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53344)에서 제공됩니다.
    - Linux의 경우 [Linux - 지원되는 플랫폼](../linux/sql-server-linux-setup.md#supportedplatforms)을 참조하세요.

## <a name="sql-server-installation-may-fail-if-ssms-18x-is-installed"></a>SSMS 18.x가 설치된 경우 SQL Server 설치가 실패할 수 있음

- **문제 및 고객에게 미치는 영향**: 다음과 같은 조건에서는 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 설치가 실패합니다.
  1. SSMS(SQL Server Management Studio) 버전 18.0, 18.1, 18.2 또는 18.3이 서버에 설치되어 있습니다.
  1. 이동식 미디어에서 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 설치를 시도합니다. 예를 들어 설치 미디어가 DVD입니다.

- **해결 방법**:
  1. SSMS 18.3.1보다 이전 버전의 SSMS를 제거합니다.
  1. 최신 버전의 SSMS(18.3.1 이상)를 설치합니다. 최신 버전은 [SSMS 다운로드](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.
  1. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]를 정상적으로 설치합니다.

  >[!NOTE]
  >제거가 필요합니다.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 릴리스 후보.

## <a name="updated-compiler"></a>컴파일러 업데이트

- **문제 및 고객에게 미치는 영향**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]는 업데이트 컴파일러를 사용하여 빌드됩니다. CTP 2.1에서는 부동 소수점 및 다른 변환 시나리오가 업데이트된 컴파일러 때문에 이전 버전과 다른 값을 반환할 수 있다는 알려진 문제가 발생했습니다. CTP 2.2에는 영향을 받는 시나리오가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]라는 이전 버전과 동일한 결과를 반환하는지 확인하는 작업이 포함됩니다. 릴리스 후보 릴리스부터는 다른 문제가 발생하지 않았습니다. [!INCLUDE[ss2017](../includes/sssqlv14-md.md)]와 비교하여 비정상적인 결과를 즉시 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 팀](https://aka.ms/sqlfeedback)에게 보고해주세요.

- **해결 방법**: 해당 사항 없음

- **적용 대상**: 릴리스 후보

## <a name="installation-wizard-may-wait-between-eula-pages"></a>EULA 페이지가 넘어갈 때마다 설치 마법사가 잠시 멈출 수 있습니다.

- **문제 및 고객에게 미치는 영향**: 설치 마법사를 사용하여 설치하는 동안 R Services에 대한 EULA(최종 사용자 사용권 계약)와 Python에 대한 EULA 사이에 오랜 시간 동안 멈출 수 있습니다.

- **해결 방법**: 설치 마법사가 다시 계속될 때까지 기다립니다. 기다리는 시간은 30분을 초과할 수 있습니다.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0

## <a name="utf-8-collations"></a>UTF-8 데이터 정렬

- **문제 및 고객에게 미치는 영향**: UTF-8 사용 데이터 정렬을 다른 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능과 함께 사용할 수 없습니다. UTF-8은 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능이 사용 중일 때 지원되지 않습니다.

  - 메모리 내 OLTP
  - PolyBase용 외부 테이블([!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 1)
  - Always Encrypted(최대 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 1)
  - 연결된 서버(최대 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2)

  > [!Note]
  > 현재 Azure Data Studio 또는 SSDT(SQL Server Data Tools)에서 UTF-8 사용 데이터 정렬을 선택하도록 UI를 지원하지 않습니다. 최신 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)](SSMS) 버전 18은 UI의 다양한 UTF-8 사용 데이터 정렬 선택을 지원합니다.
 
- **해결 방법**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP에 대한 해결 방법은 없습니다.


- **적용 대상**: 모든 CTP 릴리스.

## <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted

- **문제 및 고객에게 미치는 영향**: 풍부한 컴퓨팅은 보류 중인 성능 최적화 및 오류 처리 개선 사항이며, 현재 기본적으로 사용하지 않도록 설정되어 있습니다.

- **해결 방법**: 리치 계산을 사용하도록 설정하려면 `DBCC traceon(127,-1)`을 실행합니다. 자세한 내용은 [풍부한 컴퓨팅사용](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave)을 참조하세요.

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2, CTP 3.1

## <a name="sql-server-configuration-manager-may-not-start"></a>SQL Server 구성 관리자가 시작하지 않을 수도 있습니다.

- **문제 및 고객에게 미치는 영향**: VCRuntime 140(VCRUNTIME140.dll) 파일이 없는 머신에서는 SSCM(SQL Server 구성 관리자)이 시작되지 않습니다. SSCM을 시작할 때 다음 대화 상자가 표시될 수 있습니다. 


  `MMC could not create the snap-in. The snap-in might not have been installed correctly.`

- **해결 방법**:  최신 VC 런타임 2013(x86)를 설치하세요.

  - [Verbose](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
  - [수동으로 설치](https://support.microsoft.com/help/4032938/update-for-visual-c-2013-redistributable-package)

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.1, CTP 3.0, CTP 2.5.

## <a name="always-on-availability-group-kubernetes-operator-not-supported"></a>Always On 가용성 그룹 Kubernetes 연산자는 지원되지 않음

- **문제 및 고객에게 미치는 영향**: Always On 가용성 그룹에 대한 Kubernetes 연산자는 이 릴리스 후보에서 지원되지 않으며 RTM에서 사용할 수 없습니다. 

- **해결 방법**: 없음

- **적용 대상**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 릴리스 후보

## <a name="master-data-service-notification-email-contains-broken-link"></a>Master Data Service 알림 메일에 끊어진 링크가 포함됨

- **문제 및 고객에게 미치는 영향**: MDS(Master Data Services)의 알림 메일에 끊어진 링크가 있습니다. 링크를 클릭하면 다음 메시지와 같은 오류를 반환하는 페이지로 이동됩니다.

   `The view 'Index' or its master was not found or no view engine supports the searched locations.`

- **해결 방법**: MDS 포털을 열고 리소스로 직접 이동합니다.

- **적용 대상**: SQL Server 2019 릴리스 후보

## <a name="machine-learning-services"></a>Machine Learning Services

SQL Server Machine Learning Services의 문제는 [SQL Server Machine Learning Services의 알려진 문제](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)를 참조하세요.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)

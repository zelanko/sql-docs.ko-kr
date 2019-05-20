---
title: SQL Server(CEIP) 사용 현황 및 진단 데이터 수집 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: configuration
ms.openlocfilehash: 44a8d6c22d7dd003f7c6e90963eb546e6ca1bf50
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65372753"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-ceip"></a>SQL Server(CEIP) 사용 현황 및 진단 데이터 수집 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="summary"></a>요약

기본적으로 Microsoft SQL Server는 고객이 애플리케이션을 사용하는 방법에 대한 정보를 수집합니다. 특히, SQL Server는 설치 환경, 사용 및 성능에 대한 정보를 수집합니다. 이 정보는 Microsoft에서 고객의 요구에 맞게 제품을 향상시키는 데 도움이 됩니다. 예를 들어 Microsoft는 관련 버그를 수정하고, SQL Server 사용 방법에 대한 설명서를 개선하고, 고객에게 더 나은 서비스를 제공하기 위해 제품에 기능을 추가할지 여부를 결정할 수 있도록 고객에게 발생하는 오류 코드 종류에 대한 정보를 수집합니다.

특히 Microsoft는 이러한 메커니즘을 통해 다음과 같은 유형의 정보는 전송하지 않습니다.
- 사용자 테이블 내부의 값
- 로그온 자격 증명 또는 기타 인증 정보
- PII(개인 식별 정보)

다음 예제 시나리오는 제품을 개선하는 데 도움이 되는 기능 사용 정보를 포함합니다.

SQL Server 2017은 빠른 분석 시나리오를 위해 ColumnStore 인덱스를 지원합니다. ColumnStore 인덱스는 새로 삽입한 데이터에 대한 "B-트리" 인덱스 구조를 특수한 열 기반 압축 구조와 결합하여 데이터를 압축하고 쿼리 실행 속도를 높입니다. 이 제품에는 백그라운드에서 B-트리 구조의 데이터를 압축된 구조로 마이그레이션하기 위한 추론이 포함되어 있으므로 향후 쿼리 결과가 더 빠르게 제공될 수 있을 것입니다.

백그라운드 작업이 데이터 삽입 속도와 맞지 않을 경우 쿼리 성능이 예상보다 오래 걸릴 수 있습니다. 제품을 개선하기 위해 Microsoft는 SQL Server가 자동 데이터 압축 프로세스 속도를 얼마나 잘 따라가는지에 대한 정보를 수집합니다. 제품 팀은 이 정보를 사용하여 압축을 수행하는 코드의 빈도 및 병렬 처리를 구체적으로 조정합니다. Microsoft에서 데이터 이동 속도를 평가할 수 있도록 경우에 따라 이 정보를 수집하기 위해 다음 쿼리가 실행됩니다. 이 쿼리는 제품 추론을 최적화하는 데 도움이 됩니다.  

```sql
SELECT object_id, type_desc, data_space_id, db_id() AS database_id FROM sys.indexes WITH(nolock) WHERE type = 5 or type = 6 
```

```sql
SELECT cntr_value as merge_policy_evaluation
FROM sys.dm_os_performance_counters WITH(nolock)
WHERE object_name LIKE '%columnstore%' 
AND counter_name ='Total Merge Policy Evaluations' 
AND instance_name = '_Total'
```

이 프로세스는 고객에게 가치를 전달하는 데 필요한 메커니즘에 중점을 둡니다. 제품 팀은 인덱스의 데이터를 확인하거나 해당 데이터를 Microsoft에 전송하지 않습니다. SQL Server 2017은 고객이 경험하는 설치 문제를 빠르게 찾아 해결할 수 있도록 하기 위해 항상 설치 프로세스에서 설치 환경에 대한 정보를 수집하고 전송합니다. 다음 메커니즘을 통해 Microsoft에 정보를 전송하지 않도록 SQL Server 2017을 구성할 수 있습니다(서버 인스턴스 기준).
- 오류 및 사용 보고 애플리케이션 사용
- 서버에서 레지스트리 하위 키 설정

Linux의 SQL Server에 대해서는 [Linux의 SQL Server에 대한 고객 의견](https://docs.microsoft.com/sql/linux/sql-server-linux-customer-feedback)을 참조하세요.

> [!NOTE]
> 유료 버전의 SQL Server에서만 Microsoft로 정보를 보내지 못하게 설정할 수 있습니다.

## <a name="remarks"></a>Remarks
 - SQL CEIP 서비스 제거 또는 비활성화는 지원되지 않습니다. 
 - 클러스터 그룹에서 SQL CEIP 리소스를 제거하는 것은 지원되지 않습니다. 

데이터 수집을 옵트아웃하려면 [로컬 감사 켜기 또는 끄기](usage-and-diagnostic-data-in-local-audit.md#turning-local-audit-on-or-off)를 참조하세요.

## <a name="error-and-usage-reporting-application"></a>오류 및 사용 보고 애플리케이션 

설치 후에 SQL Server 구성 요소 및 인스턴스에 대한 사용 현황 및 진단 데이터 수집 설정을 오류 및 사용 보고 애플리케이션을 통해 변경할 수 있습니다. 이 애플리케이션은 SQL Server 설치의 일부로 사용할 수 있습니다. 이 도구를 사용하면 각 SQL Server 인스턴스에서 자체 사용 보고서 설정을 구성할 수 있습니다.

> [!NOTE]
> SQL Server의 구성 도구에서 오류 및 사용 보고 애플리케이션이 나열됩니다. SQL Server 2017의 경우와 같은 방식으로 이 도구를 사용하여 오류 보고와 사용 현황 및 진단 데이터 수집에 대한 기본 설정을 관리할 수 있습니다. 오류 보고는 사용 현황 및 진단 데이터 수집과는 별개이므로, 사용 현황 및 진단 데이터 수집과는 별도로 켜거나 끌 수 있습니다. 오류 보고는 Microsoft로 전송되며 [개인정보처리방침](https://go.microsoft.com/fwlink/?LinkID=868444)에 설명된 중요한 정보를 포함할 수 있는 크래시 덤프를 수집합니다.

SQL Server 오류 및 사용 보고를 시작하려면 **시작**을 클릭하거나 누르고 검색 상자에서 "오류"를 검색합니다. SQL Server 오류 및 사용 보고 항목이 표시 됩니다. 이 도구를 시작한 후 해당 컴퓨터에 설치된 인스턴스 및 구성 요소에 대해 수집된 사용 현황 및 진단 데이터와 심각한 오류를 관리할 수 있습니다.

유료 버전의 경우 "사용 보고서" 확인란을 사용하여 Microsoft로의 사용 현황 및 진단 데이터 보내기를 관리합니다.

유료 또는 평가 버전에 대해 "오류 보고서" 확인란을 사용하여 Microsoft에 심각한 오류 및 크래시 덤프 관련 의견을 전송하는 것을 관리합니다.

## <a name="set-registry-subkeys-on-the-server"></a>서버에서 레지스트리 하위 키 설정

엔터프라이즈 고객은 사용 현황 및 진단 데이터 수집에 참여하거나 참여하지 않도록 그룹 정책 설정을 구성할 수 있습니다. 이 작업은 레지스트리 기반 정책을 구성하여 수행합니다. 관련 레지스트리 하위 키와 설정은 다음과 같습니다.

- SQL Server 인스턴스 기능:
    
    하위 키 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE
    
    레지스트리 항목 이름 = CustomerFeedback
    
    항목 종류 DWORD: 0은 참여하지 않음. 1은 참여함
    
    {InstanceID}은(는) 다음 예제와 같이 인스턴스 유형 및 인스턴스를 나타냅니다.

    - SQL Server 2017 데이터베이스 엔진의 경우 MSSQL14.CANBERRA, 인스턴스 이름 "CANBERRA"
    - SQL Server 2017 Analysis Services의 경우 MSAS14.CANBERRA, 인스턴스 이름 "CANBERRA"
    - SQL Server 2017 Reporting Services의 경우 MSRS14.CANBERRA, 인스턴스 이름 "CANBERRA"

- 모든 공유 기능:
    
    하위 키 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}
    
    레지스트리 항목 이름 = CustomerFeedback
    
    항목 종류 DWORD: 0은 참여하지 않음. 1은 참여함

> [!NOTE]
> {Major Version}은 SQL Server 버전을 나타냄(예: SQL Server 2017의 경우는 140)

- SQL Server Management Studio 17 및 SQL Server Management Studio 18의 경우 [SQL Server Management Studio의 사용자 지원](../ssms/sql-server-management-studio-telemetry-ssms.md)을 참조하세요.

## <a name="set-registry-subkeys-for-crash-dump-collection"></a>크래시 덤프 수집에 대한 레지스트리 하위 키 설정

이전 버전의 SQL Server에서 나타난 동작과 마찬가지로, SQL Server 2017 Enterprise 고객은 크래시 덤프 수집에 참여 또는 참여하지 않도록 서버의 그룹 정책 설정을 구성할 수 있습니다. 이 작업은 레지스트리 기반 정책을 구성하여 수행합니다. 관련 레지스트리 키와 설정은 다음과 같습니다. 

- SQL Server 인스턴스 기능:

    하위 키 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE

    레지스트리 항목 이름 = EnableErrorReporting

    항목 종류 DWORD: 0은 참여하지 않음. 1은 참여함
 
    {InstanceID}은(는) 다음 예제와 같이 인스턴스 유형 및 인스턴스를 나타냅니다. 

    - SQL Server 2017 데이터베이스 엔진의 경우 MSSQL14.CANBERRA, 인스턴스 이름 "CANBERRA"
    - SQL Server 2017 Analysis Services의 경우 MSAS14.CANBERRA, 인스턴스 이름 "CANBERRA"
    - SQL Server 2017 Reporting Services의 경우 MSRS14.CANBERRA, 인스턴스 이름 "CANBERRA"
 

- 모든 공유 기능:
    
    하위 키 = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}

    레지스트리 항목 이름 = EnableErrorReporting

    항목 종류 DWORD: 0은 참여하지 않음. 1은 참여함

> [!NOTE]
> {Major Version}은 SQL Server 버전을 나타냅니다. 예를 들어 SQL Server 2017의 경우는 “140”입니다.

이러한 레지스트리 하위 키에 대한 레지스트리 기반 그룹 정책은 SQL Server 2017 크래시 덤프 수집에 따라 적용됩니다. 

## <a name="crash-dump-collection-for-ssms"></a>SSMS에 대한 크래시 덤프 수집
SSMS는 자체 크래시 덤프를 수집하지 않습니다. SSMS와 관련된 모든 크래시 덤프는 Windows 오류 보고의 일부로 수집됩니다.

이 기능을 설정하거나 해제하는 절차는 OS 버전에 따라 달라집니다. 이 기능을 설정하거나 해제하려면 사용하는 Windows 버전에 대한 문서에 포함된 단계를 따르세요.
 
- Windows Server 2016 및 Windows 10

    [조직에서 Windows 진단 데이터 구성](https://docs.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization)
- Windows Server 2008 R2 및 Windows 7

    [WER 설정](/windows/desktop/wer/wer-settings)
 
## <a name="feedback-for-analysis-services"></a>Analysis Services에 대한 피드백

설치 중에 SQL Server 2016 Analysis Services는 Analysis Services 인스턴스에 특수 계정을 추가합니다. 이 계정은 Analysis Services 서버 관리자 역할의 구성원입니다. 이 계정은 Analysis Services 인스턴스에서 피드백에 대한 정보를 수집하는 데 사용됩니다.  

"서버에서 레지스트리 하위 키 설정" 섹션에 설명된 대로 사용 현황 및 진단 데이터를 전송하지 않도록 서비스를 구성할 수 있습니다. 그러나 이렇게 해도 서비스 계정은 제거되지 않습니다. 
 
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

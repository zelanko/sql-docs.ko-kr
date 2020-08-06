---
title: 보안 Enclave를 사용한 Always Encrypted
description: SQL Server에 보안 enclave 기능을 사용하는 Always Encrypted를 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 27ccecb8293adff8fe5f2aaa3062a871d745c587
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435447"
---
# <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]
 
보안 Enclave를 사용한 Always Encrypted는 [Always Encrypted](always-encrypted-database-engine.md) 기능에 추가 기능을 제공합니다.

SQL Server 2016에 도입된, Always Encrypted는 맬웨어 및 높은 권한이 있는 SQL Server *무단* 사용자로부터 중요한 데이터의 기밀을 보호합니다. 높은 권한이 있는 무단 사용자는 DBA, 컴퓨터 관리자, 클라우드 관리자 또는 서버 인스턴스에 대해 합법적인 액세스 권한이 있지만 실제 데이터의 일부 또는 전체에 대해 액세스 권한이 없는 사람입니다.  

이 문서에 설명된 향상된 기능을 사용하지 않는 Always Encrypted는 클라이언트 쪽에서 데이터를 암호화하여 데이터 또는 해당 암호화 키가 SQL Server 엔진 내에서 일반 텍스트로 표시되지 않도록 함으로써 데이터를 보호합니다. 따라서 데이터베이스 내에 있는 암호화된 열에 대한 기능이 심각하게 제한됩니다. SQL Server가 암호화된 데이터에 관해 수행할 수 있는 유일한 작업은 같음 비교입니다(결정적 암호화에서만 사용할 수 있음). 암호화 작업(초기 데이터 암호화 또는 키 회전), 리치 계산(예: 패턴 일치) 등 다른 모든 작업은 데이터베이스 내에서 지원되지 않습니다. 사용자가 클라이언트 쪽에서 해당 작업을 수행하려면 데이터베이스 외부로 데이터를 이동해야 합니다.

*보안 Enclave를 사용한* Always Encrypted는 서버 쪽의 보안 Enclave 내에서 일반 텍스트 데이터에 대한 계산을 허용하여 이러한 제한을 해결합니다. 보안 Enclave는 SQL Server 프로세스 내의 보호된 메모리 영역으로, SQL Server 엔진 내에서 중요한 데이터를 처리하기 위한 신뢰할 수 있는 실행 환경으로 사용됩니다. 보안 Enclave는 SQL Server의 나머지 부분 및 호스팅 컴퓨터의 다른 프로세스에서 불투명 상자로 표시됩니다. 디버거를 사용하더라도 외부에서 Enclave 내의 데이터나 코드를 볼 수 없습니다.  


Always Encrypted는 다음 다이어그램에 설명된 것처럼 보안 Enclave를 사용합니다.

![데이터 흐름](./media/always-encrypted-enclaves/ae-data-flow.png)



애플리케이션의 쿼리를 구문 분석할 때 SQL Server 엔진은 쿼리가 보안 Enclave를 사용해야 하는 암호화된 데이터에 대한 작업을 포함하는지 확인합니다. 보안 Enclave를 액세스해야 하는 쿼리:

- 클라이언트 드라이버는 작업에 필요한 열 암호화 키를 보안 채널을 통해 보안 Enclave로 보냅니다. 
- 그러면 클라이언트 드라이버는 암호화된 쿼리 매개 변수와 함께 실행할 쿼리를 제출합니다.

쿼리 처리 동안, 데이터 또는 열 암호화 키는 보안 Enclave 외부의 SQL Server 엔진에서 일반 텍스트로 노출되지 않습니다. SQL Server 엔진은 암호화된 열의 암호화 작업 및 계산을 보안 enclave에 위임합니다. 필요한 경우, 보안 Enclave는 암호화된 열에 저장된 쿼리 매개 변수 및/또는 데이터의 암호를 해독하고 요청된 작업을 수행합니다.

[!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]에서 보안 Enclave를 사용한 Always Encrypted는 Windows의 [VBS(가상화 기반 보안)](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) 보안 메모리 Enclave(가상 보안 모드 또는 VSM Enclave라고도 함)를 사용합니다.

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted를 사용하는 이유는 무엇일까요?

보안 Enclaves를 사용하면 Always Encrypted는 다음과 같은 이점을 제공하면서 중요한 데이터의 기밀성을 보호합니다.

- **바로 암호화** – 중요한 데이터에 대한 암호화 작업(예: 초기 데이터 암호화 또는 열 암호화 키 순환)은 보안 Enclave 내에서 수행되며 데이터베이스 외부로 데이터를 이동할 필요가 없습니다. ALTER TABLE Transact-SQL 문을 사용하여 바로 암호화를 실행할 수 있으며, SSMS의 Always Encrypted 마법사 또는 Set-SqlColumnEncryption PowerShell cmdlet과 같은 도구를 사용할 필요가 없습니다.

- **리치 계산** – 패턴 일치(LIKE 조건자) 및 범위 비교를 비롯하여 암호화된 열에 대해 수행되는 작업은 보안 Enclave 내에서 지원됩니다. 이 경우 데이터베이스 시스템 내에서 이러한 계산을 수행하도록 요구하는 광범위한 애플리케이션 및 시나리오가 Always Encrypted에서 지원됩니다.

## <a name="secure-enclave-attestation"></a>보안 Enclave 증명

SQL Server 엔진 내의 보안 Enclave는 암호화된 데이터베이스 열에 저장된 중요한 데이터와 일반 텍스트로 나타낸 해당 열 암호화 키에 액세스할 수 있습니다. Enclave 계산을 포함하는 쿼리를 SQL Server로 제출하기 전에, 애플리케이션 내의 클라이언트 드라이버는 지정된 기술(예: VBS)에 따라 보안 Enclave가 정품 Enclave인지 확인하고, Enclave 내에서 실행되는 코드가 Enclave 내에서 실행될 수 있게 서명되었는지 확인해야 합니다. 

Enclave를 확인하는 프로세스를 **Enclave 증명**이라고 하며, 애플리케이션 내의 클라이언트 드라이버와 SQL Server가 둘 다 외부 증명 서비스에 연결합니다. 증명 프로세스의 사양은 Enclave 기술과 증명 서비스에 따라 좌우됩니다.

[!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]에서 SQL Server가 VBS 보안 Enclave를 지원하는 증명 프로세스를 Windows Defender System Guard 런타임 증명이라고 하며 이 프로세스는 HGS(호스트 보호 서비스)를 증명 서비스로 사용합니다. 사용자 환경에서 HGS를 구성하고 HGS에서 SQL Server 인스턴스를 호스트하는 컴퓨터를 등록해야 합니다. 또한 HGS 증명을 사용하여 클라이언트 애플리케이션 또는 도구(예: SQL Server Management Studio)를 구성해야 합니다.

## <a name="supported-client-drivers"></a>지원되는 클라이언트 드라이버

보안 Enclave를 사용한 Always Encrypted를 사용하려면 애플리케이션은 해당 기능을 지원하는 클라이언트 드라이버를 사용해야 합니다. 애플리케이션 및 클라이언트 드라이버에서 Enclave 계산 및 Enclave 증명을 사용하도록 구성해야 합니다. 지원되는 클라이언트 드라이버 목록을 비롯한 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)를 참조하세요.

## <a name="enclave-enabled-keys"></a>Enclave 사용 키

보안 Enclave를 사용한 Always Encrypted는 Enclave 사용 키의 개념을 도입했습니다.

- **Enclave 사용 열 마스터 키** – 데이터베이스 내의 열 마스터 키 메타데이터 개체에 ENCLAVE_COMPUTATIONS 속성이 지정된 열 마스터 키입니다. 열 마스터 키 메타데이터 개체는 메타데이터 속성의 유효한 서명도 포함해야 합니다.
- **Enclave 사용 열 암호화 키** – Enclave 사용 열 마스터 키로 암호화된 열 암호화 키입니다.

SQL Server 엔진은 쿼리에 지정된 작업을 보안 Enclave 내에서 수행해야 한다고 결정하면 클라이언트 드라이버에 계산에 필요한 열 암호화 키를 보안 Enclave와 공유하도록 요청합니다. 클라이언트 드라이버는 열 암호화 키가 enclave 사용 키(즉, Enclave 사용 열 마스터 키로 암호화됨)이고 적절히 서명된 경우에만 해당 키를 공유합니다. 그렇지 않으면 쿼리는 실패합니다.

자세한 내용은 [Manage keys for Always Encrypted with secure enclaves](always-encrypted-enclaves-manage-keys.md)(보안 Enclave를 사용한 Always Encrypted 키 관리)를 참조하세요.

## <a name="enclave-enabled-columns"></a>Enclave 사용 열

Enclave 사용 열은 Enclave 사용 열 암호화 키로 암호화한 데이터베이스 열입니다. Enclave 사용 열에 사용할 수 있는 기능은 열이 사용하는 암호화 유형에 따라 다릅니다.

- **결정적 암호화** - 결정적 암호화를 사용하는 Enclave 사용 열은 바로 암호화를 지원하지만 보안 Enclave 내에서 다른 작업은 지원하지 않습니다. 같음 비교는 지원되지만 enclave 외부에서 암호 텍스트를 비교하여 수행됩니다.  
- **임의 암호화** - 임의 암호화를 사용하는 Enclave 사용 열은 보안 Enclave 내에서 바로 암호화 및 리치 계산을 모두 지원합니다. 지원되는 리치 계산은 패턴 일치 및 [비교 연산자](../../../t-sql/language-elements/comparison-operators-transact-sql.md)(같음 비교 포함)입니다.

암호화 유형에 대한 자세한 내용은 [Always Encrypted 암호화](always-encrypted-cryptography.md)를 참조하세요.

다음 표에서는 열이 Enclave 사용 열 암호화 키 및 암호화 유형을 사용하는지 여부에 따라 암호화된 열에 사용할 수 있는 기능을 요약해서 보여 줍니다.

| **연산**| **열이 Enclave 사용 열이 아님** |**열이 Enclave 사용 열이 아님**| **열이 Enclave 사용 열임**.  |**열이 Enclave 사용 열임**. |
|:---|:---|:---|:---|:---|
| | **임의 암호화**  | **결정적 암호화**     | **임의 암호화**      | **결정적 암호화**     |
| **바로 암호화** | 지원되지 않음  | 지원되지 않음   | 지원됨         | 지원됨    |
| **같음 비교**   | 지원되지 않음 | Enclave 외부에서 지원됨 | 지원됨(Enclave 내부) | Enclave 외부에서 지원됨 |
| **같음에 대한 비교 연산자** | 지원되지 않음  | 지원되지 않음   | 지원됨      | 지원되지 않음     |
| **LIKE**    | 지원되지 않음      | 지원되지 않음    | 지원됨     | 지원되지 않음    |

바로 암호화는 Enclave 내에서 다음 작업을 지원합니다.

- 기존 열에 저장된 데이터의 초기 암호화
- 열에 있는 기존 데이터 다시 암호화(예:
  
  - 열 암호화 키 순환(새 키로 열을 다시 암호화)
  - 암호화 유형 변경  

- 암호화된 열에 저장된 데이터 암호 해독(열을 일반 텍스트 열로 변환)

바로 암호화가 가능하려면 암호화 작업에 관련된 열 암호화 키가 Enclave 사용 키여야 합니다.

- 초기 암호화: 암호화할 열의 열 암호화 키가 Enclave 사용 키여야 합니다.
- 다시 암호화: 현재 및 대상 열 암호화 키(현재 키와 다른 경우)가 Enclave 사용 키여야 합니다.
- 암호 해독: 열의 현재 열 암호화 키가 Enclave 사용 키여야 합니다.

### <a name="indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>임의 암호화를 사용하는 Enclave 사용 열의 인덱스
풍부한 쿼리가 더 빠르게 실행되도록 임의 암호화를 이용하여 enclave 사용 열에 비클러스터형 인덱스를 만들 수 있습니다. 임의 암호화를 사용하여 암호화된 열의 인덱스에는 중요한 데이터를 누출하지 않는 동시에, enclave 내의 쿼리 처리에 유용합니다. 인덱스 데이터 구조(B-트리)의 키 값이 암호화되고 해당 일반 텍스트 값에 따라 정렬됩니다. SQL Server 엔진의 쿼리 실행기가 enclave 내의 계산을 위해 암호화된 열의 인덱스를 사용하는 경우 인덱스를 검색하여 열에 저장된 특정 값을 조회합니다. 각 검색에서 여러 개의 비교를 수행할 수 있습니다. 쿼리 실행기는 각 비교를 enclave에 위임하고, enclave는 열에 저장된 값 및 비교할 암호화된 인덱스 키 값의 암호를 해독하고 일반 텍스트를 비교하여 비교 결과를 실행기에 반환합니다. 

임의 암호화를 사용하는데 enclave를 지원하지 않는 열에는 인덱스를 만들 수 없습니다.

자세한 내용은 [보안 Enclave를 사용한 Always Encrypted를 이용하여 열에 인덱스 만들기 및 사용](always-encrypted-enclaves-create-use-indexes.md)을 참조하세요. Always Encrypted와 관련된 정보가 아닌, SQL Server 인덱싱의 작동 방식에 대한 일반적인 내용은 [클러스터형 및 비클러스터형 인덱스 소개](../../indexes/clustered-and-nonclustered-indexes-described.md)를 참조하세요.

#### <a name="database-recovery"></a>데이터베이스 복구

SQL Server 인스턴스에서 오류가 발생하면 데이터베이스가 불완전한 트랜잭션으로 인한 수정 내용이 데이터 파일에 포함된 상태로 남겨질 수 있습니다. 인스턴스를 시작하면 트랜잭션 로그에서 발견된 불완전한 트랜잭션을 모두 롤백하여 데이터베이스의 무결성을 유지하는 [데이터베이스 복구](../../logs/the-transaction-log-sql-server.md#recovery-of-all-incomplete-transactions-when--is-started) 프로세스가 실행됩니다. 불완전한 트랜잭션이 인덱스를 변경한 경우 해당 변경 내용도 취소해야 합니다. 예를 들어 인덱스의 일부 키 값을 제거하거나 다시 삽입해야 할 수 있습니다.

> [!IMPORTANT]
> 데이터베이스에 대해 [ADR(가속 데이터베이스 복구)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr)을 사용하도록 설정한 **다음**, 임의 암호화로 암호화된 enclave 사용 열에 첫 번째 인덱스를 만드는 것이 좋습니다.

인덱스의 변경 내용을 취소하는 [기존 데이터베이스 복구 프로세스](https://docs.microsoft.com/azure/sql-database/sql-database-accelerated-database-recovery#the-current-database-recovery-process)([ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf) 복구 모델을 따름)에서는 애플리케이션이 열의 열 암호화 키를 enclave에 제공할 때까지 SQL Server에서 기다려야 하며, 오랜 시간이 걸릴 수 있습니다. ADR을 사용하면 enclave 내부 캐시에서 열 암호화 키를 사용할 수 없어 지연되어야 하는 실행 취소 작업 수가 훨씬 줄어듭니다. 따라서 새 트랜잭션이 차단될 가능성이 최소화되어 데이터베이스 가용성이 상당히 증가합니다. ADR을 사용하는 경우에도 SQL Server에서 이전 데이터 버전 정리를 완료하려면 열 암호화 키가 필요할 수 있지만 백그라운드 작업으로 수행하기 때문에 데이터베이스 또는 사용자 트랜잭션의 가용성에는 영향을 주지 않습니다. 그러나 누락된 열 암호화 키로 인해 실패한 정리 작업을 나타내는 오류 메시지가 오류 로그에 표시될 수 있습니다.

### <a name="indexes-on-enclave-enabled-columns-using-deterministic-encryption"></a>결정적 암호화를 사용하는 Enclave 사용 열의 인덱스

결정적 암호화를 사용하는 열의 인덱스는 열의 enclave 사용 여부에 관계없이 암호 텍스트(일반 텍스트 아님)를 기준으로 정렬됩니다.

## <a name="security-considerations"></a>보안 고려사항

다음 보안 고려 사항은 보안 enclave를 사용한 Always Encrypted에 적용됩니다.

- enclave 내부 데이터의 보안은 증명 프로토콜 및 증명 서비스에 따라 달라집니다. 따라서 신뢰할 수 있는 관리자가 증명 서비스와 증명 서비스에서 적용하는 증명 정책을 관리하도록 해야 합니다. 또한 증명 서비스는 일반적으로 다양한 정책과 증명 프로토콜을 지원하고, 이 중에서 일부는 enclave 및 환경에 대해 최소한의 확인을 수행하며 테스트 및 개발용으로 설계되었습니다. 해당 증명 서비스와 관련된 지침에 따라 권장 구성 및 정책을 프로덕션 배포에 사용합니다. 
- 임의 암호화를 사용하는 열을 enclave 사용 CEK로 암호화하면 열 지원 범위 비교와 같은, 열에 저장된 데이터의 순서가 누출될 수 있습니다. 예를 들어 직원 급여를 포함하는 암호화된 열에 인덱스가 있는 경우, 악의적인 DBA가 인덱스를 검색하여 최대 암호화된 급여 값을 찾고 최대 급여를 받는 사람을 식별할 수 있습니다(사람 이름은 암호화되지 않았다고 가정). 
- Always Encrypted를 사용하여 DBA의 무단 액세스로부터 중요한 데이터를 보호하는 경우 열 마스터 키 또는 열 암호화 키를 DBA와 공유하지 마세요. DBA는 enclave 내부의 열 암호화 키 캐시를 활용하여 키에 직접 액세스하지 않고도 암호화된 열의 인덱스를 관리할 수 있습니다.

## <a name="considerations-for-availability-groups-and-database-migration"></a><a name="anchorname-1-considerations-availability-groups-db-migration"></a> 가용성 그룹 및 데이터베이스 마이그레이션의 고려 사항

enclave를 사용하여 쿼리를 지원하는 데 필요한 Always On 가용성 그룹을 구성하는 경우, 가용성 그룹의 데이터베이스를 호스팅하는 모든 SQL Server 인스턴스에서 보안 enclave를 사용한 Always Encrypted를 지원하며 enclave가 구성되어 있는지 확인해야 합니다. 주 데이터베이스는 enclave를 지원하지만 보조 복제본이 지원하지 않는 경우 보안 enclave를 사용한 Always Encrypted의 기능을 사용하려고 하면 실패합니다.

enclave가 구성되지 않은 SQL Server 인스턴스에서 보안 enclave를 사용한 Always Encrypted의 기능을 사용하는 데이터베이스의 백업 파일을 복원하는 경우 복원 작업이 성공하고, enclave를 이용하지 않는 모든 기능을 사용할 수 있습니다. 그러나 enclave 기능을 사용한 모든 후속 쿼리는 실패하고, 임의 암호화를 사용하는 enclave 사용 열의 인덱스가 유효하지 않게 됩니다. enclave가 구성되지 않은 인스턴스에서 보안 enclave를 사용한 Always Encrypted를 사용하는 데이터베이스를 연결하는 경우에도 동일하게 적용됩니다.

데이터베이스에 임의 암호화를 사용하는 enclave 사용 열이 포함된 경우 데이터베이스 백업을 만들기 전에 데이터베이스에서 [ADR(가속 데이터베이스 복구)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr)을 사용하도록 설정해야 합니다. ADR을 사용하면 데이터베이스를 복원한 후에 인덱스를 비롯한 데이터베이스를 즉시 사용할 수 있습니다. 자세한 내용은 [데이터베이스 복구](#database-recovery)를 참조하세요.

bacpac 파일을 사용하여 데이터베이스를 마이그레이션하는 경우, bacpac 파일을 만들기 전에 임의 암호화를 사용하는 enclave 사용 열의 인덱스를 모두 삭제해야 합니다.

## <a name="known-limitations"></a>알려진 제한 사항
보안 Enclave를 사용한 Always Encrypted는 다음 작업을 사용하도록 설정하여 Always Encrypted가 가지고 있는 제한 사항 중 일부를 해결합니다.

- 바로 암호화 작업
- 임의 암호화를 사용하여 암호화된 열의 패턴 일치(LIKE) 및 비교 연산자
    > [!NOTE]
    > 위의 작업은 binary2 정렬 순서의 데이터 정렬(BIN2 데이터 정렬)을 사용하는 문자열 열에 대해 지원됩니다. BIN2 이외의 데이터 정렬을 사용하는 문자열 열은 임의 암호화 및 Enclave 사용 열 암호화 키로 암호화할 수 있습니다. 그러나 이러한 열에 사용할 수 있는 유일한 새 기능은 바로 암호화입니다.
- 임의 암호화를 사용하는 Enclave 사용 열에 비클러스터형 인덱스 및 통계 만들기

[기능 정보](always-encrypted-database-engine.md#feature-details)에 나열된 Always Encrypted의 다른 모든 제한 사항은 보안 Enclave를 사용한 Always Encrypted에도 적용됩니다.

다음 제한 사항은 보안 enclave를 사용한 Always Encrypted와 관련이 있습니다.

- 임의 암호화를 사용하는 Enclave 사용 열에는 클러스터형 인덱스를 만들 수 없습니다.
- 임의 암호화를 사용하는 enclave 사용 열은 기본 키 열이 될 수 없으며, 외래 키 제약 조건 또는 고유 키 제약 조건에서 참조할 수 없습니다.
- 임의 암호화를 사용하는 Enclave 사용 열에서는 중첩된 루프 조인(인덱스 사용, 사용 가능한 경우)만 지원됩니다. 해시 조인과 병합 조인은 지원되지 않습니다. 
- 바로 암호화 작업은 동일한 코드 페이지 내의 데이터 정렬 및 null 허용 여부 변경을 제외하고 다른 열 메타데이터 변경과 결합할 수 없습니다. 예를 들어 단일 `ALTER TABLE`/`ALTER COLUMN` Transact-SQL 문에서 열을 암호화하거나 다시 암호화하거나 암호 해독하는 작업과 열의 데이터 형식을 변경하는 작업을 함께 수행할 수는 없습니다. 두 개의 개별 문을 사용합니다.
- 메모리 내 테이블의 열에 대해 enclave 사용 키를 사용할 수 없습니다.
- 계산 열을 정의하는 식은 임의 암호화를 사용하는 Enclave 사용 열에서 계산을 수행할 수 없습니다(계산이 LIKE 및 범위 비교인 경우에도 수행할 수 없음).
- 임의 암호화를 사용하는 Enclave 사용 열에서는 LIKE 연산자의 매개 변수에서 이스케이프 문자가 지원되지 않습니다.
- 암호화 후에 큰 개체가 되는 다음 데이터 형식 중 하나를 사용하는 쿼리 매개 변수가 있는 LIKE 연산자 또는 비교 연산자가 포함된 쿼리는 인덱스를 무시하고 테이블 검사를 수행합니다.
    - n이 3,967보다 큰 경우 `nchar[n]` 및 `nvarchar[n]`입니다.
    - n이 7,935보다 큰 경우 `char[n]`, `varchar[n]`, `binary[n]`, `varbinary[n]`입니다.
- 도구 제한 사항은 다음과 같습니다.
  - Enclave 사용 열 마스터 키를 저장할 수 있는 유일한 키 저장소는 Windows 인증서 저장소 및 Azure Key Vault입니다.
  - Enclave 사용 키가 포함된 데이터베이스 가져오기/내보내기는 지원되지 않습니다.
  - `ALTER TABLE`/`ALTER COLUMN`을 통해 바로 암호화 작업을 트리거하려면 SSMS에서 쿼리 창을 사용하여 문을 실행해야 합니다. 또는 해당 문을 실행하는 고유한 프로그램을 작성할 수도 있습니다. 현재 SqlServer PowerShell 모듈의 Set-SqlColumnEncryption cmdlet과 SQL Server Management Studio의 Always Encrypted 마법사는 바로 암호화를 지원하지 않으며, 작업에 사용되는 열 암호화 키가 Enclave 사용 키인 경우에도 암호화 작업을 위해 데이터베이스 외부로 데이터를 이동합니다.

## <a name="next-steps"></a>다음 단계
- [자습서: SSMS를 사용하여 보안 Enclave를 사용한 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [보안 Enclave를 사용한 Always Encrypted 구성 및 사용](configure-always-encrypted-enclaves.md)

## <a name="see-also"></a>참고 항목
- [보안 Enclave를 사용한 Always Encrypted 키 관리](always-encrypted-enclaves-manage-keys.md)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열 쿼리](always-encrypted-enclaves-query-columns.md)
- [기존 암호화된 열에 관해 보안 Enclave를 사용한 Always Encrypted 사용](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열에 인덱스 만들기 및 사용](always-encrypted-enclaves-create-use-indexes.md)



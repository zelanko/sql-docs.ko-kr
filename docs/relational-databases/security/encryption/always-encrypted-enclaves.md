---
title: 보안 Enclave를 사용한 Always Encrypted(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 13c15426e44ef6897cb5763d3c98f2a214298298
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814094"
---
# <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]


보안 Enclave를 사용한 Always Encrypted는 [Always Encrypted](always-encrypted-database-engine.md) 기능에 추가 기능을 제공합니다.

SQL Server 2016에 도입된, Always Encrypted는 맬웨어 및 높은 권한이 있는 SQL Server *무단* 사용자로부터 중요한 데이터의 기밀을 보호합니다. 높은 권한이 있는 무단 사용자는 DBA, 컴퓨터 관리자, 클라우드 관리자 또는 서버 인스턴스에 대해 합법적인 액세스 권한이 있지만 실제 데이터의 일부 또는 전체에 대해 액세스 권한이 없는 사람입니다. 

지금까지 Always Encrypted는 클라이언트 쪽에서 데이터를 암호화하여 데이터 또는 해당 암호화 키가 SQL Server 엔진 내에서 일반 텍스트로 표시되지 않도록 함으로써 데이터를 보호했습니다. 결과적으로, 데이터베이스 내에 있는 암호화된 열에 대한 기능은 심각하게 제한되었습니다. SQL Server가 암호화된 데이터에 대해 수행할 수 있는 유일한 작업은 같음 비교였습니다(같음 비교는 결정적 암호화를 사용할 때만 사용할 수 있음). 암호화 작업(초기 데이터 암호화 또는 키 순환) 또는 리치 계산(예: 패턴 일치)을 포함하는 모든 기타 작업은 데이터베이스 내에서 지원되지 않았습니다. 클라이언트 쪽에서 이러한 작업을 수행하려면 데이터베이스 외부로 데이터를 이동해야 했습니다.

*보안 Enclave를 사용한* Always Encrypted는 서버 쪽의 보안 Enclave 내에서 일반 텍스트 데이터에 대한 계산을 허용하여 이러한 제한을 해결합니다. 보안 Enclave는 SQL Server 프로세스 내의 보호된 메모리 영역으로, SQL Server 엔진 내에서 중요한 데이터를 처리하기 위한 신뢰할 수 있는 실행 환경으로 사용됩니다. 보안 Enclave는 SQL Server의 나머지 부분 및 호스팅 컴퓨터의 다른 프로세스에서 검은색 상자로 표시됩니다. 디버거를 사용하더라도 외부에서 Enclave 내의 데이터나 코드를 볼 수 없습니다.  


Always Encrypted는 다음 다이어그램에 설명된 것처럼 보안 Enclave를 사용합니다.

![데이터 흐름](./media/always-encrypted-enclaves/ae-data-flow.png)



응용 프로그램의 쿼리를 구문 분석할 때 SQL Server 엔진은 쿼리가 보안 Enclave를 사용해야 하는 암호화된 데이터에 대한 작업을 포함하는지 확인합니다. 보안 Enclave를 액세스해야 하는 쿼리:

- 클라이언트 드라이버는 작업에 필요한 열 암호화 키를 보안 채널을 통해 보안 Enclave로 보냅니다. 
- 그러면 클라이언트 드라이버는 암호화된 쿼리 매개 변수와 함께 실행할 쿼리를 제출합니다.

쿼리 처리 동안, 데이터 또는 열 암호화 키는 보안 Enclave 외부의 SQL Server 엔진에서 일반 텍스트로 노출되지 않습니다. SQL Server 엔진은 암호화된 열의 암호화 작업 및 계산을 보안 Enclave에 위임합니다. 필요한 경우, 보안 Enclave는 암호화된 열에 저장된 쿼리 매개 변수 및/또는 데이터의 암호를 해독하고 요청된 작업을 수행합니다.

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted를 사용하는 이유는 무엇일까요?

보안 Enclaves를 사용하면 Always Encrypted는 다음과 같은 이점을 제공하면서 중요한 데이터의 기밀성을 보호합니다.

- **바로 암호화** – 중요한 데이터에 대한 암호화 작업(예: 초기 데이터 암호화 또는 열 암호화 키 순환)은 보안 Enclave 내에서 수행되며 데이터베이스 외부로 데이터를 이동할 필요가 없습니다. ALTER TABLE Transact-SQL 문을 사용하여 바로 암호화를 실행할 수 있으며, SSMS의 Always Encrypted 마법사 또는 Set-SqlColumnEncryption PowerShell cmdlet과 같은 도구를 사용할 필요가 없습니다.

- **리치 계산(미리 보기)** – 패턴 일치(LIKE 조건자) 및 범위 비교를 비롯하여 암호화된 열에 대해 수행되는 작업은 보안 Enclave 내에서 지원됩니다. 이 경우 데이터베이스 시스템 내에서 이러한 계산을 수행하도록 요구하는 광범위한 응용 프로그램 및 시나리오가 Always Encrypted에서 지원됩니다.

> [!IMPORTANT]
> [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)]에서 리치 계산은 몇 가지 성능 최적화가 보류 중이며, 제한된 기능을 포함하고(인덱싱 없음 등), 현재 기본적으로 사용하지 않도록 설정되어 있습니다. 리치 계산을 사용하도록 설정하려면 [리치 계산 사용](configure-always-encrypted-enclaves.md#configure-a-secure-enclave)을 참조하세요.

[!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)]에서 보안 Enclave를 사용한 Always Encrypted는 Windows의 [VBS(가상화 기반 보안)](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) 보안 메모리 Enclave(가상 보안 모드 또는 VSM Enclave라고도 함)를 사용합니다.

## <a name="secure-enclave-attestation"></a>보안 Enclave 증명

SQL Server 엔진 내의 보안 Enclave는 암호화된 데이터베이스 열에 저장된 중요한 데이터와 일반 텍스트로 나타낸 해당 열 암호화 키에 액세스할 수 있습니다. Enclave 계산을 포함하는 쿼리를 SQL Server로 제출하기 전에, 응용 프로그램 내의 클라이언트 드라이버는 지정된 기술(예: VBS)에 따라 보안 Enclave가 정품 Enclave인지 확인하고, Enclave 내에서 실행되는 코드가 Enclave 내에서 실행될 수 있게 서명되었는지 확인해야 합니다. 

Enclave를 확인하는 프로세스를 **Enclave 증명**이라고 하며, 일반적으로 응용 프로그램(및 경우에 따라 SQL Server) 내의 클라이언트 드라이버가 외부 증명 서비스에 연결하게 됩니다. 증명 프로세스의 사양은 Enclave 기술과 증명 서비스에 따라 좌우됩니다.

[!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)]에서 SQL Server가 VBS 보안 Enclave를 지원하는 증명 프로세스를 Windows Defender System Guard 런타임 증명이라고 하며 이 프로세스는 HGS(호스트 보호 서비스)를 증명 서비스로 사용합니다. 사용자 환경에서 HGS를 구성하고 HGS에서 SQL Server 인스턴스를 호스트하는 컴퓨터를 등록해야 합니다. 또한 HGS 증명을 사용하여 클라이언트 응용 프로그램 또는 도구(예: SQL Server Management Studio)를 구성해야 합니다.

## <a name="secure-enclave-providers"></a>보안 Enclave 공급자

보안 Enclave를 사용한 Always Encrypted를 사용하려면 응용 프로그램은 해당 기능을 지원하는 클라이언트 드라이버를 사용해야 합니다. [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)]에서 응용 프로그램은 .NET Framework 4.7.2 및 .NET Framework Data Provider for SQL Server SQL Server를 사용해야 합니다. 또한 .NET 응용 프로그램은 사용 중인 Enclave 유형(예: VBS) 및 증명 서비스(예: HGS)에 국한되는 **보안 Enclave 공급자**로 구성해야 합니다. 지원되는 Enclave 공급자는 NuGet 패키지에 별도로 제공되므로 응용 프로그램에 통합해야 합니다. Enclave 공급자는 지정된 유형의 보안 Enclave와의 보안 채널을 설정하는 데 필요한 방식으로 증명 프로토콜에 적합하게 클라이언트 쪽 논리를 구현합니다.

## <a name="enclave-enabled-keys"></a>Enclave 사용 키

보안 Enclave를 사용한 Always Encrypted는 Enclave 사용 키의 개념을 도입했습니다.

- **Enclave 사용 열 마스터 키** – 데이터베이스 내의 열 마스터 키 메타데이터 개체에 ENCLAVE_COMPUTATIONS 속성이 지정된 열 마스터 키입니다. 열 마스터 키 메타데이터 개체는 메타데이터 속성의 유효한 서명도 포함해야 합니다.
- **Enclave 사용 열 암호화 키** – Enclave 사용 열 마스터 키로 암호화된 열 암호화 키입니다.

SQL Server 엔진은 쿼리에 지정된 작업을 보안 Enclave 내에서 수행해야 한다고 결정하면 클라이언트 드라이버에 계산에 필요한 열 암호화 키를 보안 Enclave와 공유하도록 요청합니다. 클라이언트 드라이버는 열 암호화 키가 Enclave 사용 키(즉, Enclave 사용 열 마스터 키로 암호화됨)이고 적절히 서명된 경우에만 해당 키를 공유합니다. 그렇지 않으면 쿼리는 실패합니다.

## <a name="enclave-enabled-columns"></a>Enclave 사용 열

Enclave 사용 열은 Enclave 사용 열 암호화 키로 암호화한 데이터베이스 열입니다. Enclave 사용 열에 사용할 수 있는 기능은 열이 사용하는 암호화 유형에 따라 다릅니다.

- **결정적 암호화** - 결정적 암호화를 사용하는 Enclave 사용 열은 바로 암호화를 지원하지만 보안 Enclave 내에서 다른 작업은 지원하지 않습니다. 같음 비교는 지원되지만 암호 텍스트를 비교하여(Enclave 외부) Enclave 외부에서 수행됩니다.  
- **임의 암호화** - 임의 암호화를 사용하는 Enclave 사용 열은 보안 Enclave 내에서 바로 암호화 및 리치 계산을 모두 지원합니다. 지원되는 리치 계산은 패턴 일치 및 [비교 연산자](https://docs.microsoft.com/sql/t-sql/language-elements/comparison-operators-transact-sql)(같음 비교 포함)입니다.

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

## <a name="known-limitations"></a>알려진 제한 사항

일반적인 제한 사항: 

- [기능 정보](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine#feature-details)에 나열된 최신 버전의 Always Encrypted에 대한 제한 사항이 보안 Enclave를 사용한 Always Encrypted(Enclave 사용 키로 암호화한 열)에도 적용됩니다. 단, 바로 암호화 및 리치 계산에 대한 지원 추가로 일부 제한이 제거되었습니다.

- 같음 비교는 결정적 암호화에서 지원되는 유일한 Transact-SQL 연산자이며, 같음 비교는 열 암호화 키가 Enclave 사용 키인지 여부에 관계없이 Enclave 외부에서 암호 텍스트 값을 비교하여 수행됩니다. 결정적 암호화를 위한 Enclave 사용 열 암호화 키로 잠금이 해제되는 유일한 새 기능은 바로 암호화 작업입니다. 리치 계산(패턴 일치, 비교 연산)을 사용하기 위해 결정적 암호화를 사용하여 암호화한 열(및 Enclave 사용 키가 아닌 키)이 있는 경우 임의 암호화를 사용하여 열을 다시 암호화해야 합니다.

- 데이터 정렬 사용에 대한 기존 제한이 Enclave 사용 열 암호화 키로 암호화한 열에도 적용됩니다. 즉, 결정적 암호화를 사용하여 암호화한 문자열 열(char, nchar, varchar, nvarchar)은 binary2 정렬 순서를 갖는 데이터 정렬(BIN2 데이터 정렬)을 사용해야 합니다. BIN2 이외의 데이터 정렬을 사용하는 문자열 열은 임의 암호화를 사용하여 암호화할 수 있지만, 이러한 열(Enclave 사용 열 암호화 키로 암호화한 경우)에 사용하도록 설정된 유일한 새 기능은 바로 암호화입니다. **리치 계산(패턴 일치, 비교 연산)을 지원하려면 열이 BIN2 데이터 정렬을 사용해야 합니다**(또한 열은 임의 암호화 및 Enclave 사용 열 암호화 키를 사용하여 암호화해야 함).

- 메모리 내 테이블의 열에 대해 Enclave 사용 키를 사용하는 것은 지원되지 않습니다.

- 바로 암호화 작업은 데이터 정렬 및 null 허용 여부 변경을 제외하고 어떠한 열 메타데이터 변경과도 조합할 수 없습니다. 예를 들어, 단일 ALTER TABLE 또는 ALTER COLUMN Transact-SQL 문에서 열 암호화, 다시 암호화 또는 암호 해독을 수행하는 작업과 열의 데이터 형식을 변경하는 작업을 함께 수행할 수 없습니다. 두 개의 별도 명령문을 사용해야 합니다.

다음과 같은 제한 사항이 현재 미리 보기에 적용되지만 해결 중입니다.

- 임의 암호화를 사용하는 Enclave 사용 열은 인덱싱할 수 없습니다. 즉, 비교 연산 또는 LIKE 연산에는 테이블 검색이 필요합니다.

- 보안 Enclave를 사용한 Always Encrypted를 지원하는 유일한 클라이언트 드라이버는 .NET Framework 4.7.2의 .NET Framework Data Provider for SQL Server(ADO.NET)입니다. ODBC/JDBC 지원이 없습니다.

- Enclave 사용 열 마스터 키를 저장할 수 있는 유일한 키 저장소는 Windows 인증서 저장소 및 Azure Key Vault입니다.

- 보안 Enclave를 사용한 Always Encrypted에 대한 도구 지원은 현재 완료되지 않았습니다. ALTER TABLE Transact-SQL 문을 통해 바로 암호화 작업을 트리거하기 위해서는 SSMS에서 쿼리 창을 사용하여 문을 실행하거나, 해당 문을 실행하는 프로그램을 직접 작성할 수 있습니다. SqlServer PowerShell 모듈의 Set-sqlcolumnencryption cmdlet과 SQL Server Management Studio의 Always Encrypted 마법사는 바로 암호화를 지원하지 않지만, 작업에 사용되는 열 암호화 키가 Enclave 사용 키인 경우에도 두 도구는 암호화 작업을 위해 데이터를 데이터베이스 외부로 이동합니다. 

## <a name="known-issues"></a>알려진 문제

- 비유니코드(char, varchar) 문자열 열에 대해 리치 계산을 수행하려면 BIN2 데이터 정렬이 데이터베이스 수준에서 설정되어야 합니다. [데이터 정렬 관리](configure-always-encrypted-enclaves.md#manage-collations)에서 비유니코드 문자열 열에 대한 특별 고려 사항을 참조하세요.

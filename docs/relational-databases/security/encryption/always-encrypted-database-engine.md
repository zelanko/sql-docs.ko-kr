---
title: Always Encrypted | Microsoft Docs
description: SQL Server 및 Azure SQL Database에서 투명한 클라이언트 쪽 암호화 및 기밀 컴퓨팅을 지원하는 Always Encrypted의 개요
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], Always Encrypted
- Always Encrypted
- TCE Always Encrypted
- Always Encrypted, about
- SQL13.SWB.COLUMNMASTERKEY.CLEANUP.F1
ms.assetid: 54757c91-615b-468f-814b-87e5376a960f
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1f097d500c1d1b0a035f2bb0e737214d65803414
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477724"
---
# <a name="always-encrypted"></a>Always Encrypted
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

  ![Always Encrypted](../../../relational-databases/security/encryption/media/always-encrypted.png "Always Encrypted")  
  
 상시 암호화는 신용 카드 번호나 주민 등록 번호(예: 미국 사회 보장 번호)와 같이 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 저장된 중요한 데이터를 보호하기 위한 기능입니다. 상시 암호화를 사용하면 클라이언트가 클라이언트 애플리케이션의 중요한 데이터를 암호화하고 암호화 키를 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] ([!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)])에 표시하지 않을 수 있습니다. 따라서 Always Encrypted는 데이터를 소유하고 볼 수 있는 사람과 데이터를 관리하지만 액세스 권한이 없어야 하는 사람을 분리합니다. 온-프레미스 데이터베이스 관리자, 클라우드 데이터베이스 관리자 또는 기타 높은 권한을 가지고 있지만 인증되지 않은 사용자가 암호화된 데이터에 액세스할 수 없도록 함으로써 Always Encrypted는 고객이 직접 제어할 수 없는 중요한 데이터를 안전하게 저장하도록 해줍니다. 이를 통해 조직에서는 데이터를 Azure에 저장하기 위해 암호화하고 온-프레미스 데이터베이스 관리를 타사에 위임할 수 있도록 하거나, 자체 DBA 직원에 대한 보안 정보 사용 허가 요구 사항을 줄일 수 있습니다.

 Always Encrypted는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에서 암호화된 데이터에 대한 일부 쿼리를 처리할 수 있도록 하고, 데이터의 기밀성을 유지하고, 위의 보안 이점을 제공하여 기밀 컴퓨팅 기능을 제공합니다. [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[sssSQLv14](../../../includes/sssqlv14-md.md)]에서 그리고 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]에서 Always Encrypted는 결정적 암호화를 통해 같음 비교를 지원합니다. [결정적 암호화 또는 임의 암호화 선택](#selecting--deterministic-or-randomized-encryption)을 참조하세요. 

  > [!NOTE] 
  > [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]에서 보안 enclave는 패턴 일치, 기타 비교 연산자 및 내부 암호화를 사용하여 Always Encrypted의 기밀 컴퓨팅 기능을 크게 확장합니다. [보안 enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)를 참조하세요.

 상시 암호화는 암호화를 애플리케이션에 투명하게 만듭니다. 클라이언트 컴퓨터에 설치된 상시 암호화 지원 드라이버가 클라이언트 애플리케이션의 중요한 데이터를 자동으로 암호화하고 암호 해독합니다. 드라이버는 데이터를 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]로 전달하기 전에 중요한 열의 데이터를 암호화하고 애플리케이션에 대한 의미 체계가 유지되도록 자동으로 쿼리를 다시 작성합니다. 마찬가지로, 드라이버는 암호화된 데이터베이스 열에 저장되고 쿼리 결과에 포함된 데이터를 투명하게 암호 해독합니다.  
  
 Always Encrypted은 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]부터 모든 버전의 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)], 그리고 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]의 모든 서비스 계층에서 사용할 수 있습니다. [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] SP1 이전에는 Always Encrypted가 Enterprise Edition으로 제한되었습니다. 상시 암호화를 포함하는 Channel 9 프레젠테이션은 [상시 암호화를 사용하여 중요한 데이터의 보안 유지](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)를 참조하세요.  

  
## <a name="typical-scenarios"></a>일반적인 시나리오  
  
### <a name="client-and-data-on-premises"></a>온-프레미스 클라이언트와 데이터  
 고객은 비즈니스 위치의 온-프레미스에서 클라이언트 애플리케이션과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 모두 실행합니다. 고객은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 관리할 외부 공급업체를 고용하려고 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 저장된 중요한 데이터를 보호하기 위해 고객은 상시 암호화를 사용하여 데이터베이스 관리자와 애플리케이션 관리자 간의 업무를 분리합니다. 고객은 Always Encrypted 키의 일반 텍스트 값을 클라이언트 애플리케이션에서 액세스할 수 있는 신뢰할 수 있는 키 저장소에 저장합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관리자는 키에 대한 액세스 권한이 없으므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 저장된 중요한 데이터의 암호를 해독할 수 없습니다.  
  
### <a name="client-on-premises-with-data-in-azure"></a>온-프레미스 클라이언트와 Azure의 데이터  
 고객은 비즈니스 위치에서 온-프레미스 클라이언트 애플리케이션을 실행합니다. 애플리케이션은 Azure에서 호스트되는 데이터베이스(Microsoft Azure의 가상 머신에서 실행되는[!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)])에 저장된 중요한 데이터를 작동합니다. 고객은 상시 암호화를 사용하고 상시 암호화 키를 온-프레미스에서 호스트되는 신뢰할 수 있는 키 저장소에 저장하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 클라우드 관리자가 중요한 데이터에 액세스하지 못하도록 합니다.  
  
### <a name="client-and-data-in-azure"></a>Azure의 클라이언트와 데이터  
 고객은 Microsoft Azure(예: 작업자 역할 또는 웹 역할)에서 호스트된 클라이언트 애플리케이션을 실행합니다. 이 애플리케이션은 Azure에서 호스트된 데이터베이스(Microsoft Azure의 가상 머신에서 실행되는 SQL 데이터베이스 또는 SQL Server)에 저장된 중요한 데이터에 대해 작동합니다. Always Encrypted는 클라이언트 계층을 호스트하는 플랫폼의 클라우드 관리자에게 데이터와 키가 둘 다 노출되기 때문에 클라우드 관리자로부터 데이터를 완전히 격리하지 않지만 고객이 보안 공격 노출 영역을 줄일 수 있습니다(데이터베이스의 데이터가 항상 암호화됨).  
 
## <a name="how-it-works"></a>작동 방식

중요한 데이터를 포함하는 개별 데이터베이스 열에 대해 상시 암호화를 구성할 수 있습니다. 열에 대해 암호화를 설정하는 경우 열의 데이터를 보호하는 데 사용되는 암호화 알고리즘과 암호화 키에 대한 정보를 지정합니다. 상시 암호화는 열 암호화 키와 열 마스터 키의 두 가지 키 유형을 사용합니다. 열 암호화 키는 암호화된 열의 데이터를 암호화하는 데 사용됩니다. 열 마스터 키는 하나 이상의 열 암호화 키를 암호화하는 키 보호 키입니다. 

데이터베이스 엔진은 각 열에 대한 암호화 구성을 데이터베이스 메타데이터에 저장합니다. 그러나 데이터베이스 엔진은 어떤 유형의 키도 일반 텍스트로 저장하거나 사용하지 않습니다. Azure 주요 자격 증명 모음, 클라이언트 컴퓨터의 Windows 인증서 저장소 또는 하드웨어 보안 모듈과 같은 신뢰할 수 있는 외부 키 저장소에 저장된 열 마스터 키의 위치 정보와 열 암호화 키의 암호화된 값만 저장합니다.

암호화된 열에 저장된 데이터에 일반 텍스트로 액세스하려면 애플리케이션에서 상시 암호화 사용 클라이언트 드라이버를 사용해야 합니다. 애플리케이션에서 매개 변수가 있는 쿼리를 실행하면 드라이버가 데이터베이스 엔진과 투명하게 협력하여 암호화된 열을 대상으로 하므로 암호화해야 하는 매개 변수를 확인합니다. 암호화해야 하는 각 매개 변수에 대해 드라이버는 열 암호화 알고리즘 및 열 암호화 키의 암호화된 값, 매개 변수 대상, 해당 열 마스터 키의 위치에 대한 정보를 가져옵니다.

그런 다음, 드라이버는 암호화된 열 암호화 키 값의 암호를 해독하기 위해 열 마스터 키를 포함하는 키 저장소에 연결하고 일반 텍스트 열 암호화 키를 사용하여 매개 변수를 암호화합니다. 결과로 생성된 일반 텍스트 열 암호화 키는 이후에 동일한 열 암호화 키를 사용할 때 키 저장소로의 왕복 횟수를 줄이기 위해 캐시됩니다. 드라이버는 암호화된 열을 대상으로 하는 매개 변수의 일반 텍스트 값을 해당 암호화된 값으로 대체하고 처리를 위해 서버에 쿼리를 보냅니다.

서버가 결과 집합을 계산하고, 드라이버는 결과 집합에 포함된 암호화된 열에 대해, 암호화 알고리즘 및 해당 키에 대한 정보를 비롯한 열의 암호화 메타데이터를 연결합니다. 드라이버는 먼저 로컬 캐시에서 일반 텍스트 열 암호화 키를 찾으려고 시도하며, 캐시에서 키를 찾을 수 없는 경우에만 열 마스터 키로 왕복합니다. 그런 다음 드라이버에서 결과 암호를 해독하고 애플리케이션에 일반 텍스트 값을 반환합니다.

 클라이언트 드라이버는 열 마스터 키가 포함된 키 저장소를 캡슐화하는 클라이언트 쪽 소프트웨어 구성 요소인 열 마스터 키 저장소 공급자를 사용하여 열 마스터 키가 포함된 키 저장소와 상호 작용합니다. 일반적인 유형의 키 저장소 공급자는 Microsoft의 클라이언트 쪽 드라이버 라이브러리에서 제공되거나 독립 실행형 다운로드로 제공됩니다. 또한 사용자 고유의 공급자를 구현할 수 있습니다. 기본 제공 열 마스터 키 저장소 공급자를 포함하여 Always Encrypted 기능은 드라이버 라이브러리와 해당 버전에 따라 다릅니다. 

특정 클라이언트 드라이버와 함께 Always Encrypted를 사용하여 애플리케이션을 개발하는 방법은 [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)을 참조하세요.

## <a name="remarks"></a>설명

암호화 및 암호 해독은 클라이언트 드라이버를 통해 발생합니다. 즉, Always Encrypted를 사용하는 경우 서버 쪽에서만 발생하는 일부 작업이 작동하지 않습니다. 예제에는 UPDATE, BULK INSERT(T-SQL), SELECT INTO, INSERT..SELECT를 통해 한 열에서 다른 열로 데이터를 복사하는 작업이 포함됩니다. 

클라이언트에 결과 집합을 반환하지 않고 암호화된 열에서 암호화되지 않은 열로 데이터를 이동하려는 UPDATE의 예제는 다음과 같습니다. 

```sql
update dbo.Patients set testssn = SSN
```

SSN이 Always Encrypted를 사용한 암호화 열이면 위의 업데이트 문은 다음과 유사한 오류를 표시하며 실패합니다.

```
Msg 206, Level 16, State 2, Line 89
Operand type clash: char(11) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_1', column_encryption_key_database_name = 'ssn') collation_name = 'Latin1_General_BIN2' is incompatible with char
```

열을 성공적으로 업데이트하려면 다음을 수행합니다.

1. SSN 열에서 데이터를 선택하고, 애플리케이션에 결과 집합으로 저장합니다. 이렇게 하면 애플리케이션(클라이언트 *드라이버*)이 열 암호를 해독할 수 있습니다.
2. 결과 집합에서 SQL Server로 데이터를 삽입합니다. 

 >[!IMPORTANT]
 > 이 시나리오에서 대상 열이 암호화된 데이터를 허용하지 않는 일반 varchar이기 때문에 데이터는 서버에 다시 보낼 때 암호화됩니다. 
  
## <a name="selecting-deterministic-or-randomized-encryption"></a><a name="selecting--deterministic-or-randomized-encryption"></a> 결정적 암호화 또는 임의 암호화 선택  
 데이터베이스 엔진은 암호화된 열에 저장된 일반 텍스트 데이터에 대해 작동하지 않지만 열의 암호화 유형에 따라 암호화된 데이터에 대한 일부 쿼리를 지원합니다. 상시 암호화는 임의 암호화와 결정적 암호화의 두 가지 암호화 유형을 지원합니다.  
  
- 결정적 암호화는 지정된 일반 텍스트 값에 대해 항상 동일한 암호화된 값을 생성합니다. 결정적 암호화를 사용하는 경우 암호화된 열에 대한 지점 조회, 동등 조인, 그룹화 및 인덱싱이 가능합니다. 그러나 True/False 또는 북/남/동/서 지역 등 가능한 암호화된 값의 집합이 작은 경우 특히 권한이 없는 사용자가 암호화된 열의 패턴을 검사하여 암호화된 값에 대한 정보를 추측할 수도 있습니다. 결정적 암호화에서는 문자 열에 대해 binary2 정렬 순서를 적용하는 열 데이터 정렬을 사용해야 합니다.

- 임의 암호화는 예측하기 어려운 방식으로 데이터를 암호화하는 방법을 사용합니다. 임의 암호화는 더 안전하지만 암호화된 열에 대한 검색, 그룹화, 인덱싱 및 조인을 금지합니다.

검색 또는 그룹화 매개 변수로 사용할 열에는 결정적 암호화를 사용합니다. 한 예로 정부 ID 번호를 들 수 있습니다. 다른 레코드와 함께 그룹화되지 않고 테이블을 조인하는 데 사용되지 않는 기밀 조사 의견 등의 데이터에는 임의 암호화를 사용합니다.
Always Encrypted 암호화 알고리즘에 대한 자세한 내용은 [Always Encrypted 암호화](../../../relational-databases/security/encryption/always-encrypted-cryptography.md)를 참조하세요.

## <a name="configuring-always-encrypted"></a>상시 암호화 구성

 데이터베이스의 상시 암호화 초기 설정에는 상시 암호화 키 생성, 키 메타데이터 만들기, 선택한 데이터베이스 열의 암호화 속성 구성 및/또는 암호화해야 하는 열에 이미 있을 수 있는 데이터 암호화가 포함됩니다. 이러한 태스크 중 일부는 Transact-SQL에서 지원되지 않으며 클라이언트 쪽 도구를 사용해야 합니다. Always Encrypted 키 및 보호된 중요한 데이터는 일반 텍스트로 서버에 공개되지 않으므로 데이터베이스 엔진이 키 프로비저닝에 참여하여 데이터 암호화 또는 암호 해독 작업을 수행할 수 없습니다. 이러한 태스크를 수행하려면 SQL Server Management Studio 또는 PowerShell을 사용할 수 있습니다. 

|Task|SSMS|PowerShell|T-SQL|
|:---|:---|:---|:---
|열 마스터 키, 열 암호화 키 및 암호화된 열 암호화 키를 해당 열 마스터 키로 프로비전|예|예|예|
|데이터베이스에 키 메타데이터 만들기|예|예|예|
|암호화된 열이 있는 새 테이블 만들기|예|예|예|
|선택한 데이터베이스 열에 있는 기존 데이터 암호화|예|예|예|

> [!NOTE]
> [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]에 도입된 [보안 enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)는 Transact-SQL을 사용하여 기존 데이터를 암호화하는 것을 지원합니다. 또한 암호화 작업을 위해 데이터를 데이터 외부로 이동하지 않아도 됩니다.

> [!NOTE]
> 데이터베이스를 호스트하는 컴퓨터와 다른 컴퓨터의 보안 환경에서 키 프로비저닝 또는 데이터 암호화 도구를 실행해야 합니다. 그러지 않으면 중요한 데이터나 키가 서버 환경에 누출되어 상시 암호화 사용의 이점이 줄어듭니다.  

상시 암호화 구성에 대한 자세한 내용은 다음을 참조하세요.
- [SSMS를 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)

## <a name="getting-started-with-always-encrypted"></a>상시 암호화 시작

[상시 암호화 마법사](../../../relational-databases/security/encryption/always-encrypted-wizard.md) 를 사용하여 상시 암호화 사용을 빠르게 시작할 수 있습니다. 마법사는 필요한 키를 프로비전하고 선택한 열에 대한 암호화를 구성합니다. 암호화를 설정할 열에 일부 데이터가 이미 포함되어 있으면 마법사에서 데이터를 암호화합니다. 다음 예제에서는 열을 암호화하는 프로세스를 보여 줍니다.

> [!NOTE]  
>  마법사 사용이 포함된 동영상을 보려면 [SSMS를 사용하여 상시 암호화 시작](https://channel9.msdn.com/Shows/Data-Exposed/Getting-Started-with-Always-Encrypted-with-SSMS)을 참조하세요.

1.  Management Studio의 **개체 탐색기** 를 사용하여 암호화할 열이 있는 테이블을 포함하는 기존 데이터베이스에 연결하거나, 새 데이터베이스를 만들고 암호화할 열이 있는 테이블을 하나 이상 만든 다음 연결합니다.
2.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크** 를 가리킨 다음 **열 암호화** 를 클릭하여 **Always Encrypted 마법사** 를 엽니다.
3.  **소개** 페이지를 검토하고 **다음** 을 클릭합니다.
4.  **열 선택** 페이지에서 테이블을 확장하고 암호화할 열을 선택합니다.
5.  암호화를 위해 선택한 각 열에 대해 **암호화 유형** 을 *결정적* 또는 *임의* 로 설정합니다.
6.  암호화를 위해 선택한 각 열에 대해 **암호화 키** 를 선택합니다. 이전에 이 데이터베이스에 대한 암호화 키를 만들지 않은 경우 기본적으로 선택되는 새 자동 생성 키를 선택하고 **다음** 을 클릭합니다.
7.  **마스터 키 구성** 페이지에서 새 키를 저장할 위치를 선택하고 마스터 키 원본을 선택한 후 **다음** 을 클릭합니다.
8.  **유효성 검사** 페이지에서 스크립트를 즉시 실행할지 아니면 PowerShell 스크립트를 만들지 선택하고 **다음** 을 클릭합니다.
9.  **요약** 페이지에서 선택한 옵션을 검토하고 **마침** 을 클릭합니다. 완료되면 마법사를 닫습니다.

  
## <a name="feature-details"></a>기능 정보  
  
-   쿼리는 결정적 암호화를 사용하여 암호화된 열에서 같음 비교를 수행할 수 있지만 다른 작업(예: 보다 큼/보다 작음, LIKE 연산자를 사용한 패턴 일치 또는 산술 연산)은 수행할 수 없습니다.  
  
-   임의 암호화를 사용하여 암호화된 열에 대한 쿼리는 이러한 열에서 작업을 수행할 수 없습니다. 임의 암호화를 사용하여 암호화된 열을 인덱싱하는 기능은 지원되지 않습니다.  
 > [!NOTE] 
 > [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]에 도입된 [보안 enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)는 임의 암호화를 사용하여 열에 대한 패턴 일치, 비교 연산자 및 인덱싱을 활성화하여 위의 제한 사항을 해결합니다.

-   열 암호화 키는 각각 서로 다른 열 마스터 키로 암호화된 최대 2개의 암호화된 값을 가질 수 있습니다. 따라서 열 마스터 키 순환이 용이합니다.  
  
-   결정적 암호화를 사용하려면 열에 [*binary2* 데이터 정렬](../../../relational-databases/collations/collation-and-unicode-support.md)중 하나가 적용되어야 합니다.  

-   암호화된 개체의 정의를 변경한 후 [sp_refresh_parameter_encryption](../../../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md)을 실행하여 개체에 대한 상시 암호화 메타데이터를 업데이트합니다.
  
다음 특성이 있는 열에 대해서는 Always Encrypted가 지원되지 않습니다. 예를 들어 다음 조건 중 하나가 열에 적용되는 경우 열에 대한 `CREATE TABLE/ALTER TABLE`에서 `ENCRYPTED WITH` 절을 사용할 수 없습니다.  
  
-   다음과 같은 데이터 형식 중 하나를 사용하는 열: `xml`, `timestamp`/`rowversion`, `image`, `ntext`, `text`, `sql_variant`, `hierarchyid`, `geography`, `geometry`, 별칭, 사용자 정의 형식.  
- `FILESTREAM` 열  
- `IDENTITY` 속성이 있는 열  
- `ROWGUIDCOL` 속성이 있는 열  
- bin2가 아닌 데이터 정렬을 사용하는 문자열(`varchar`, `char` 등) 열  
- 임의 암호화를 사용하는 경우 클러스터형 및 비클러스터형 인덱스에 대한 키 역할을 하는 열(결정적 암호화 지원됨)
- 전체 텍스트 인덱스에 포함된 열(Always Encrypted는 [전체 텍스트 검색](../../../relational-databases/search/full-text-search.md)을 지원하지 않음)  
- 계산된 열입니다.
- 계산된 열에서 참조되는 열(식이 Always Encrypted에 대해 지원되지 않는 작업을 수행하는 경우)  
- 스파스 열 집합  
- 임의 암호화를 사용하는 경우 통계에서 참조되는 열(결정적 암호화 지원됨)  
- 별칭 형식을 사용하는 열  
- 분할 열  
- 기본 제약 조건이 있는 열  
- 임의 암호화를 사용하는 경우 고유한 제약 조건에서 참조되는 열(결정적 암호화도 지원됨)  
- 임의 암호화를 사용하는 경우 기본 키 열(결정적 암호화도 지원됨)  
- 임의 암호화를 사용하거나 결정적 암호화를 사용할 때 참조된 열과 참조하는 열에서 서로 다른 키 또는 알고리즘을 사용하는 경우 외래 키 제약 조건에서 참조하는 열  
- CHECK 제약 조건에서 참조되는 열  
- 변경 데이터 캡처를 사용하여 캡처되는/추적되는 열  
- 변경 내용 추적을 사용하는 테이블의 기본 키 열  
- 마스킹된 열(동적 데이터 마스킹 사용)  
- 스트레치 데이터베이스 테이블의 열 상시 암호화로 암호화된 열이 있는 테이블은 스트레치에 사용할 수 있습니다.  
- 외부(PolyBase) 테이블의 열(참고: 암호화된 열이 있는 테이블과 외부 테이블을 같은 쿼리에서 사용할 수 있음).  
- 암호화된 열을 대상으로 하는 테이블 반환 매개 변수는 지원되지 않습니다.  

다음 절은 암호화된 열에 사용할 수 없습니다.

- `FOR XML`
- `FOR JSON PATH`

다음 기능은 암호화된 열에서 작동하지 않습니다.

- 트랜잭션 또는 병합 복제
- 분산 쿼리(연결된 서버, `OPENROWSET`(T-SQL), `OPENDATASOURCE`(T-SQL))

도구 요구 사항

- 암호화된 열에서 검색된 결과의 암호를 해독하거나 암호화된 열을 삽입, 업데이트 또는 필터링하는 쿼리를 실행하는 데는 SQL Server Management Studio 버전 18 이상이 권장됩니다. 
- `sqlcmd` 버전 13.1 이상이 필요합니다([다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=825643)에서 사용할 수 있음).

  
## <a name="database-permissions"></a>데이터베이스 권한  
 상시 암호화에 대한 다음 4가지 사용 권한이 있습니다.  
  
*  `ALTER ANY COLUMN MASTER KEY` (열 마스터 키를 만들고 삭제하는 데 필요합니다.)  
  
*  `ALTER ANY COLUMN ENCRYPTION KEY` (열 암호화 키를 만들고 삭제하는 데 필요합니다.) 
  
*  `VIEW ANY COLUMN MASTER KEY DEFINITION` (키를 관리하거나 암호화된 열을 쿼리하기 위해 열 마스터 키의 메타데이터를 액세스하고 읽는 데 필요합니다.)  
  
*  `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` (키를 관리하거나 암호화된 열을 쿼리하기 위해 열 암호화 키의 메타데이터를 액세스하고 읽는 데 필요합니다.)  
  
 다음 표에는 일반적인 작업에 필요한 사용 권한이 요약되어 있습니다.  
  
|시나리오|<code>ALTER ANY COLUMN MASTER KEY</code>|<code>ALTER ANY COLUMN ENCRYPTION KEY</code>|<code>VIEW ANY COLUMN MASTER KEY DEFINITION</code>|<code>VIEW ANY COLUMN ENCRYPTION KEY DEFINITION</code>|  
|--------------|-----------------------------------|---------------------------------------|---------------------------------------------|-------------------------------------------------|  
|키 관리(데이터베이스에서 키 메타데이터 만들기/변경/검토)|X|X|X|X|  
|암호화된 열 쿼리|||X|X|  
  
 **중요 정보:**  
  
-   사용 권한은 [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] (대화 상자 및 마법사) 또는 PowerShell을 사용한 작업에 적용됩니다.  
  
-   암호화된 열을 선택하는 경우 사용자에게 열의 암호를 해독할 수 있는 권한이 없어도 두 개의 *보기* 권한이 필요합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 두 개의 *보기* 권한이 `public` 고정 데이터베이스 역할에 기본적으로 모두 부여됩니다. 데이터베이스 관리자는 *역할에 대한* 보기 `public` 권한을 해지(또는 거부)하고 특정 역할이나 사용자에게 부여하여 보다 제한적인 제어를 구현할 수 있습니다.  
  
-   [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서는 *보기* 권한이 `public` 고정 데이터베이스 역할에 기본적으로 부여되지 않습니다. 이렇게 하면 기존의 특정 레거시 도구(이전 버전의 DacFx 사용)가 제대로 작동할 수 있습니다. 따라서 암호화된 열로 작업하려면(암호를 해독하지 않는 경우에도) 데이터베이스 관리자가 두 개의 *보기* 권한을 명시적으로 부여해야 합니다.  

  
## <a name="example"></a>예제  
 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 은 열 마스터 키 메타데이터, 열 암호화 키 메타데이터 및 암호화된 열이 있는 테이블을 만듭니다. 메타데이터에서 참조된 키를 만드는 방법은 다음을 참조하세요.
- [SSMS를 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)

  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = 'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
---------------------------------------------  
CREATE COLUMN ENCRYPTION KEY MyCEK   
WITH VALUES  
(  
    COLUMN_MASTER_KEY = MyCMK,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x01700000016C006F00630061006C006D0061006300680069006E0065002F006D0079002F003200660061006600640038003100320031003400340034006500620031006100320065003000360039003300340038006100350064003400300032003300380065006600620063006300610031006300284FC4316518CF3328A6D9304F65DD2CE387B79D95D077B4156E9ED8683FC0E09FA848275C685373228762B02DF2522AFF6D661782607B4A2275F2F922A5324B392C9D498E4ECFC61B79F0553EE8FB2E5A8635C4DBC0224D5A7F1B136C182DCDE32A00451F1A7AC6B4492067FD0FAC7D3D6F4AB7FC0E86614455DBB2AB37013E0A5B8B5089B180CA36D8B06CDB15E95A7D06E25AACB645D42C85B0B7EA2962BD3080B9A7CDB805C6279FE7DD6941E7EA4C2139E0D4101D8D7891076E70D433A214E82D9030CF1F40C503103075DEEB3D64537D15D244F503C2750CF940B71967F51095BFA51A85D2F764C78704CAB6F015EA87753355367C5C9F66E465C0C66BADEDFDF76FB7E5C21A0D89A2FCCA8595471F8918B1387E055FA0B816E74201CD5C50129D29C015895CD073925B6EA87CAF4A4FAF018C06A3856F5DFB724F42807543F777D82B809232B465D983E6F19DFB572BEA7B61C50154605452A891190FB5A0C4E464862CF5EFAD5E7D91F7D65AA1A78F688E69A1EB098AB42E95C674E234173CD7E0925541AD5AE7CED9A3D12FDFE6EB8EA4F8AAD2629D4F5A18BA3DDCC9CF7F352A892D4BEBDC4A1303F9C683DACD51A237E34B045EBE579A381E26B40DCFBF49EFFA6F65D17F37C6DBA54AA99A65D5573D4EB5BA038E024910A4D36B79A1D4E3C70349DADFF08FD8B4DEE77FDB57F01CB276ED5E676F1EC973154F86  
);  
---------------------------------------------  
CREATE TABLE Customers (  
    CustName nvarchar(60)   
        COLLATE  Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,  
        ENCRYPTION_TYPE = RANDOMIZED,  
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'),   
    SSN varchar(11)   
        COLLATE  Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,  
        ENCRYPTION_TYPE = DETERMINISTIC ,  
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'),   
    Age int NULL  
);  
GO  
  
```  
## <a name="see-also"></a>참고 항목  
- [SSMS를 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)   
- [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)   
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md) 
- [Always Encrypted 마법사를 사용하여 열 암호화 구성](always-encrypted-wizard.md)
- [Always Encrypted 암호화](../../../relational-databases/security/encryption/always-encrypted-cryptography.md)   
- [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md)   
- [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
- [CREATE TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql.md)   
- [column_definition &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-column-definition-transact-sql.md)   
- [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)  
- [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
- [sys.column_master_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
- [sys.columns&#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
- [sp_refresh_parameter_encryption&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md)   
  
  

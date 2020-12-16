---
title: SQL Server Management Studio를 사용하여 Always Encrypted 키 순환 | Microsoft Docs
description: SQL Server Management Studio를 사용하여 Always Encrypted 열 마스터 키 및 열 암호화 키를 순환하는 작업을 알아봅니다.
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
- sql13.SWB.COLUMNMASTERKEY.CLEANUP.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 09be06fc9f84b46a93363c8386b492f987872583
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463104"
---
# <a name="rotate-always-encrypted-keys-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Always Encrypted 키 순환
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

이 문서에서는 [SSMS(SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md)를 사용하여 Always Encrypted 열 마스터 키 및 열 암호화 키를 순환하는 작업을 설명합니다.

모범 사례, 권장 사항 및 중요한 보안 고려 사항을 비롯한 Always Encrypted 키 관리의 개요는 [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.

<a name="rotatecmk"></a>
## <a name="rotate-column-master-keys"></a>열 마스터 키 순환 

열 마스터 키 순환은 기존 열 마스터 키를 새 열 마스터 키로 대체하는 프로세스입니다. 키가 손상된 경우 또는 암호화 키를 정기적으로 순환하도록 요구하는 조직의 정책이나 규정 준수 규칙을 준수하기 위해 키를 순환해야 할 수 있습니다. 열 마스터 키 순환에서는 현재 열 마스터 키로 보호된 열 암호화 키의 암호를 해독하고 새 열 마스터 키를 사용하여 다시 암호화한 다음 키 메타데이터를 업데이트합니다. 

### <a name="step-1-provision-a-new-column-master-key"></a>1단계: 새 열 마스터 키 프로비전

[새 열 마스터 키 대화 상자를 사용하여 열 마스터 키 프로비전](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)의 단계를 수행합니다.

### <a name="step-2-encrypt-column-encryption-keys-with-the-new-column-master-key"></a>2단계: 새 열 마스터 키로 열 암호화 키 암호화

열 마스터 키는 일반적으로 하나 이상의 열 암호화 키를 보호합니다. 각 열 암호화 키에는 데이터베이스에 저장된 암호화된 값이 있으며 열 마스터 키로 열 암호화 키를 암호화하는 제품입니다.
이 단계에서는 순환할 열 마스터 키로 보호된 각 열 암호화 키를 새 열 마스터 키로 암호화하고 새로 암호화된 값을 데이터베이스에 저장합니다. 따라서 순환의 영향을 받는 각 열 암호화 키에는 기존 열 마스터 키로 암호화된 값과 새 열 마스터 키로 암호화된 새 값의 두 가지 암호화된 값이 있습니다.

1.  **개체 탐색기** 를 사용하여 **보안>Always Encrypted 키>열 마스터 키** 폴더로 이동한 다음 순환할 열 마스터 키를 찾습니다.
2.  열 마스터 키를 마우스 오른쪽 단추로 클릭하고 **순환** 을 선택합니다.
3.  **열 마스터 키 순환** 대화 상자의 **대상** 필드에서, 1단계에서 만든 새 열 마스터 키의 이름을 선택합니다.
4.  기존 열 마스터 키로 보호되는 열 암호화 키의 목록을 검토합니다. 이러한 키에 회전이 적용됩니다.
5.  **확인** 을 클릭합니다.

SQL Server Management Studio에서 이전 열 마스터 키로 보호된 열 암호화 키의 메타데이터와 이전 및 새 열 마스터 키의 메타데이터를 가져옵니다. 그런 다음 SSMS는 열 마스터 키 메타데이터를 사용하여 이전 열 마스터 키가 포함된 키 저장소에 연결하고 열 암호화 키의 암호를 해독합니다. 이후에 SSMS는 새 열 마스터 키가 포함된 키 저장소에 액세스하여 열 암호화 키의 새로 암호화된 값 집합을 생성한 다음 새 값을 메타데이터에 추가합니다( [ALTER COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 문 생성 및 실행).

> [!NOTE]
> 이전 열 마스터 키로 암호화된 각 열 암호화 키가 다른 열 마스터 키로 암호화되지 않도록 합니다. 즉, 회전이 적용되는 각 열 암호화 키는 데이터베이스에 정확히 하나의 암호화된 값만 포함해야 합니다. 영향을 받는 열 암호화 키에 암호화된 값이 두 개 이상 있는 경우 순환을 진행하기 전에 값을 제거해야 합니다(열 암호화 키의 암호화된 값을 제거하는 방법은 *4단계* 참조).

### <a name="step-3-configure-your-applications-with-the-new-column-master-key"></a>3단계: 새 열 마스터 키로 애플리케이션 구성

이 단계에서는 순환할 열 마스터 키로 보호된 데이터베이스 열(즉, 순환할 열 마스터 키로 암호화된 열 암호화 키로 암호화된 데이터베이스 열)을 쿼리하는 모든 클라이언트 애플리케이션이 새 열 마스터 키에 액세스할 수 있는지 확인해야 합니다. 이 단계는 새 열 마스터 키가 있는 키 저장소의 유형에 따라 달라집니다. 예를 들면 다음과 같습니다.

- 새 열 마스터 키가 Windows 인증서 저장소에 저장된 인증서인 경우 데이터베이스에서 열 마스터 키의 키 경로에 지정된 위치와 동일한 인증서 저장소 위치(*현재 사용자* 또는 *로컬 컴퓨터*)에 인증서를 배포해야 합니다. 애플리케이션에서 인증서에 액세스할 수 있어야 합니다.
  - 인증서가 *현재 사용자* 인증서 저장소 위치에 저장된 경우 인증서를 애플리케이션 Windows ID(사용자)의 현재 사용자 저장소로 가져와야 합니다.
  - 인증서가 *로컬 컴퓨터* 인증서 저장소 위치에 저장된 경우 애플리케이션의 Windows ID에 인증서에 액세스할 권한이 있어야 합니다.
- 새 열 마스터 키가 Microsoft Azure 주요 자격 증명 모음에 저장된 경우 애플리케이션이 Azure에 인증할 수 있고 키에 대한 액세스 권한이 있도록 애플리케이션을 구현해야 합니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)을 참조하세요.

> [!NOTE]
> 순환의 이 시점에서는 이전 열 마스터 키와 새 열 마스터 키가 모두 유효하며 데이터에 액세스하는 데 사용할 수 있습니다.

### <a name="step-4-clean-up-column-encryption-key-values-encrypted-with-the-old-column-master-key"></a>4단계: 이전 열 마스터 키로 암호화된 열 암호화 키 값 정리

새 열 마스터 키를 사용하도록 모든 애플리케이션을 구성했으면 데이터베이스에서 *이전* 열 마스터 키로 암호화된 열 암호화 키 값을 제거합니다. 이전 값을 제거하면 다음 순환을 수행할 준비가 된 것입니다(순환할 열 마스터 키로 보호된 각 열 암호화 키에 정확히 하나의 암호화된 값이 있어야 함).

이전 열 마스터 키를 보관 또는 제거하기 전에 이전 값을 정리하는 다른 이유는 성능 때문입니다. 암호화된 열을 쿼리할 때 상시 암호화 가능 클라이언트 드라이버가 두 값(이전 값과 새 값)의 암호를 모두 해독해야 할 수도 있습니다. 드라이버는 애플리케이션 환경에서 두 열 마스터 키 중 어떤 것이 유효한지 모르기 때문에 서버에서 암호화된 두 값을 모두 검색합니다. 사용 불가능한 열 마스터 키로 보호되기 때문에 값 중 하나의 암호 해독에 실패하는 경우(예: 저장소에서 제거된 이전 열 마스터 키) 드라이버는 새 열 마스터 키를 사용하여 다른 값의 암호 해독을 시도합니다.

> [!WARNING]
> 애플리케이션에 해당 열 마스터 키가 제공되기 전에 열 암호화 키 값을 제거하면 애플리케이션에서 데이터베이스 열의 암호를 더 이상 해독할 수 없습니다.

1.  **개체 탐색기** 를 사용하여 **보안>상시 암호화 키** 폴더로 이동한 다음 대체할 기존 열 마스터 키를 찾습니다.
2.  기존 열 마스터 키를 마우스 오른쪽 단추로 클릭하고 **정리** 를 선택합니다.
3.  제거할 열 암호화 키 값의 목록을 검토합니다.
4.  **확인** 을 클릭합니다.

SQL Server Management Studio에서 [ALTER COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 문을 실행하여 이전 열 마스터 키로 암호화된 열 암호화 키의 암호화된 값을 삭제합니다.

### <a name="step-5-delete-metadata-for-your-old-column-master-key"></a>5단계: 이전 열 마스터 키에 대한 메타데이터 삭제

데이터베이스에서 이전 열 마스터 키의 정의를 제거하도록 선택한 경우 아래 단계를 따르세요.

1. **개체 탐색기** 를 사용하여 **보안>상시 암호화 키>열 마스터 키** 폴더로 이동한 다음 데이터베이스에서 제거할 이전 열 마스터 키를 찾습니다.
2. 이전 열 마스터 키를 마우스 오른쪽 단추로 클릭하고 **삭제** 를 선택합니다. 이렇게 하면 [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) 문이 생성 및 실행되어 열 마스터 키 메타데이터를 제거합니다.
3. **확인** 을 클릭합니다.

> [!NOTE]
> 순환 후에 이전 열 마스터 키를 영구적으로 삭제하지 않는 것이 좋습니다. 대신, 이전 열 마스터 키를 현재 키 저장소에 유지하거나 다른 안전한 장소에 보관해야 합니다. 백업 파일에서 새 열 마스터 키가 구성되기 전의 시점으로 데이터베이스를 복원하는 경우 데이터에 액세스하려면 이전 키가 필요합니다.

### <a name="permissions-for-rotating-column-master-key"></a>열 마스터 키를 순환할 수 있는 권한

열 마스터 키를 순환하려면 다음과 같은 데이터베이스 사용 권한이 있어야 합니다.

- **ALTER ANY COLUMN MASTER KEY** – 새 열 마스터 키에 대한 메타데이터를 만들고 이전 열 마스터 키에 대한 메타데이터를 삭제하는 데 필요합니다.
- **ALTER ANY COLUMN ENCRYPTION KEY** - 열 암호화 키 메타데이터를 수정하고 새로 암호화된 값을 추가하는 데 필요합니다.

또한 키 저장소에서 이전 열 마스터 키와 새 열 마스터 키를 모두 액세스할 수 있어야 합니다. 키 저장소에 액세스하고 열 마스터 키를 사용하려면 키 저장소 또는/및 키에 대한 사용 권한이 필요할 수 있습니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure Key Vault** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 *create*, *get*, *unwrapKey*, *wrapKey*, *sign* 및 *verify* 권한이 필요합니다.
- **CNG(키 저장소 공급 기업)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급 기업)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)을 참조하세요.

<a name="rotatecek"></a> 
## <a name="rotate-column-encryption-keys"></a>열 암호화 키 순환

열 암호화 키를 순환하려면 모든 열에서 순환할 키로 암호화된 데이터의 암호를 해독하고 새 열 암호화 키를 사용하여 데이터를 다시 암호화해야 합니다.

>[!NOTE]
> 순환할 키로 암호화된 열을 포함하는 테이블이 크면 열 암호화 키를 순환하는 데 시간이 오래 걸릴 수 있습니다. 데이터를 다시 암호화하는 동안에는 애플리케이션이 영향을 받는 테이블에 쓸 수 없습니다. 따라서 조직에서 열 암호화 키 순환을 계획할 때는 주의해야 합니다.
열 암호화 키를 순환하려면 상시 암호화 마법사를 사용합니다.

1.  데이터베이스에 대한 마법사를 엽니다. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업** 을 가리킨 다음 **열 암호화** 를 클릭합니다.
2.  **소개** 페이지를 검토하고 **다음** 을 클릭합니다.
3.  **열 선택** 페이지에서 테이블을 확장하고 이전 열 암호화 키로 현재 암호화된, 바꾸려는 열을 모두 찾습니다.
4.  이전 열 암호화 키로 암호화된 각 열에 대해 **암호화 키** 를 자동 생성된 새 키로 설정합니다. **참고:** 또는 마법사를 실행하기 전에 새 열 암호화 키를 만들 수 있습니다. 위의 [새 열 암호화 키 대화 상자를 사용하여 열 암호화 키 프로비전](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)을 참조하세요.
5.  **마스터 키 구성** 페이지에서 새 키를 저장할 위치를 선택하고 마스터 키 원본을 선택한 후 **다음** 을 클릭합니다. **참고:** 자동 생성된 열 암호화 키가 아니라 기존 열 암호화 키를 사용하는 경우에는 이 페이지에서 수행할 작업이 없습니다.
6.  **유효성 검사** 페이지에서 스크립트를 즉시 실행할지 아니면 PowerShell 스크립트를 만들지 선택하고 **다음** 을 클릭합니다.
7.  **요약** 페이지에서 선택한 옵션을 검토하고 **마침** 을 클릭합니다. 완료되면 마법사를 닫습니다.
8.  **개체 탐색기** 를 사용하여 **보안/상시 암호화 키/열 암호화 키** 폴더로 이동한 다음 데이터베이스에서 제거할 이전 열 암호화 키를 찾습니다. 키를 마우스 오른쪽 단추로 클릭하고 **삭제** 를 선택합니다.

### <a name="permissions-for-rotating-column-encryption-keys"></a>열 암호화 키를 순환할 수 있는 권한

열 암호화 키를 순환하려면 다음과 같은 데이터베이스 사용 권한이 있어야 합니다. **ALTER ANY COLUMN MASTER KEY** – 자동 생성된 새 열 암호화 키를 사용하는 경우에 필요합니다(새 열 마스터 키와 새 메타데이터도 생성됨).
**ALTER ANY COLUMN ENCRYPTION KEY** – 새 열 암호화 키에 대한 메타데이터를 추가하는 데 필요합니다.

또한 새 열 암호화 키와 이전 열 암호화 키 둘 다의 열 마스터 키에 액세스할 수 있어야 합니다. 키 저장소에 액세스하고 열 마스터 키를 사용하려면 키 저장소 또는/및 키에 대한 사용 권한이 필요할 수 있습니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure Key Vault** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 get, unwrapKey 및 verify 권한이 필요합니다.
- **CNG(키 저장소 공급 기업)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급 기업)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [Always Encrypted를 위한 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
- [SQL Server Management Studio로 Always Encrypted를 사용하여 열 쿼리](always-encrypted-query-columns-ssms.md)
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)

## <a name="see-also"></a>참고 항목
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted를 위한 키 관리 개요](overview-of-key-management-for-always-encrypted.md) 
- [SQL Server Management Studio를 사용하여 Always Encrypted 구성](configure-always-encrypted-using-sql-server-management-studio.md)
- [PowerShell을 사용하여 Always Encrypted 구성](configure-always-encrypted-using-powershell.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY(Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)

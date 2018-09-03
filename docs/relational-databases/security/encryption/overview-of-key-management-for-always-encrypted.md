---
title: 상시 암호화를 위한 키 관리 개요 | Microsoft 문서
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 07a305b1-4110-42f0-b7aa-28a4e32e912a
caps.latest.revision: 32
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1bf32549d66721d74c1b8eaad6bda13093e7a1a2
ms.sourcegitcommit: 010755e6719d0cb89acb34d03c9511c608dd6c36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240121"
---
# <a name="overview-of-key-management-for-always-encrypted"></a>상시 암호화를 위한 키 관리 개요
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


[상시 암호화](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)는 사용자 데이터를 암호화하는 키와 데이터를 암호화하는 키를 암호화하는 다른 키 등 두 가지 유형의 암호화 키를 사용하여 데이터를 보호합니다. 열 암호화 키는 사용자 데이터를 암호화하고, 열 마스터 키는 열 암호화 키를 암호화합니다. 이 문서에서는 이러한 암호화 키 관리의 개요를 자세히 설명합니다.

상시 암호화 키와 키 관리를 설명할 때는 실제 암호화 키와 키를 *설명* 하는 메타데이터 개체 간의 차이를 이해하는 것이 중요합니다. **열 암호화 키** 와 **열 마스터 키** 라는 용어는 실제 암호화 키를 가리키고, **열 암호화 키 메타데이터** 와 **열 마스터 키 메타데이터** 라는 용어는 데이터베이스의 상시 암호화 키 *설명* 을 가리킵니다.

- ***열 암호화 키*** 는 데이터를 암호화하는 데 사용되는 콘텐츠 암호화 키입니다. 이름에서 알 수 있듯이 열 암호화 키를 사용하여 데이터베이스 열의 데이터를 암호화합니다. 동일한 열 암호화 키를 사용하여 하나 이상의 열을 암호화하거나, 응용 프로그램 요구 사항에 따라 여러 개의 열 암호화 키를 사용할 수 있습니다. 열 암호화 키 자체가 암호화되며, 열 암호화 키의 암호화된 값만 열 암호화 키 메타데이터의 일부로 데이터베이스에 저장됩니다. 열 암호화 키 메타데이터는 [sys.column_encryption_keys(TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) 및 [sys.column_encryption_key_values(TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) 카탈로그 뷰에 저장됩니다. AES-256 알고리즘에서 사용되는 열 암호화 키는 256비트입니다.


- ***열 마스터 키*** 는 열 암호화 키를 암호화하는 데 사용되는 키를 보호하는 키입니다. 열 마스터 키는 Windows 인증서 저장소, Azure 주요 자격 증명 모음, 하드웨어 보안 모듈 등의 신뢰할 수 있는 키 저장소에 저장해야 합니다. 데이터베이스에는 열 마스터 키에 대한 메타데이터(키 저장소 유형 및 위치)만 포함됩니다. 열 마스터 키 메타데이터는 [sys.column_master_keys(TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md) 카탈로그 뷰에 저장됩니다.  

데이터베이스 시스템의 키 메타데이터에는 일반 텍스트 열 마스터 키 또는 일반 텍스트 열 암호화 키가 포함되지 않습니다. 데이터베이스에는 열 마스터 키의 유형 및 위치와 열 암호화 키의 암호화된 값에 대한 정보만 포함됩니다. 즉, 데이터베이스 시스템이 손상된 경우에도 상시 암호화를 사용하여 보호된 데이터가 안전하도록 일반 텍스트 키는 데이터베이스 시스템에 노출되지 않습니다. 데이터베이스 시스템이 일반 텍스트 키에 액세스할 수 없게 하려면 데이터베이스를 호스트하는 컴퓨터 이외의 다른 컴퓨터에서 키 관리 도구를 실행해야 합니다. 자세한 내용은 아래 [키 관리에 대한 보안 고려 사항](#SecurityForKeyManagement) 섹션을 참조하세요.

데이터베이스에는 암호화된 데이터(상시 암호화로 보호된 열)만 포함되며 일반 텍스트 키에 액세스할 수 없으므로 데이터 암호를 해독할 수 없습니다. 즉, 상시 암호화 열을 쿼리하면 암호화된 값만 반환되므로 보호된 데이터를 암호화하거나 암호를 해독해야 하는 클라이언트 응용 프로그램이 열 마스터 키 및 관련된 열 암호화 키에 액세스할 수 있어야 합니다. 자세한 내용은 [상시 암호화(클라이언트 개발)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)를 참조하세요.



## <a name="key-management-tasks"></a>키 관리 태스크

키 관리 프로세스는 다음과 같은 상위 수준 태스크로 나누어질 수 있습니다.

- **키 프로비저닝** - 신뢰할 수 있는 키 저장소(예: Windows 인증서 저장소, Azure 주요 자격 증명 모음 또는 하드웨어 보안 모듈)에 물리적 키 만들기, 열 마스터 키를 사용하여 열 암호화 키 암호화, 데이터베이스에 두 가지 유형의 키에 대한 메타데이터 만들기

- **키 순환** - 정기적으로 기존 키를 새 키로 교체 키가 손상된 경우 또는 암호화 키를 순환하도록 요구하는 조직의 정책이나 규정 준수 규칙을 준수하기 위해 키를 순환해야 할 수 있습니다. 


## <a name="KeyManagementRoles"></a> 키 관리 역할

상시 암호화 키를 관리하는 두 가지 사용자 역할이 있으며, 보안 관리자와 DBA(데이터베이스 관리자)입니다.

- **보안 관리자** - 열 암호화 키와 열 마스터 키를 생성하고 열 마스터 키를 포함하는 키 저장소를 관리합니다. 이러한 태스크를 수행하려면 보안 관리자가 키와 키 저장소에 액세스할 수 있어야 하지만 데이터베이스에 액세스할 필요는 없습니다.
- **DBA** – 데이터베이스의 키 메타데이터를 관리합니다. 키 관리 태스크를 수행하려면 DBA가 데이터베이스의 키 메타데이터를 관리할 수 있어야 하지만 키 또는 열 마스터 키를 포함하는 키 저장소에 액세스할 필요는 없습니다.

위의 역할을 고려할 경우 상시 암호화를 위한 키 관리 태스크를 수행하는 두 가지 방법이 있으며, *역할 구분 사용*및 *역할 구분 사용 안 함*입니다. 조직의 필요에 따라 요구 사항에 가장 적합한 키 관리 프로세스를 선택할 수 있습니다.

## <a name="managing-keys-with-role-separation"></a>역할 구분을 사용하여 키 관리
상시 암호화 키가 역할 구분을 사용하여 관리되는 경우 조직 내의 서로 다른 사용자가 보안 관리자 및 DBA 역할을 맡습니다. 역할 구분을 사용하는 키 관리 프로세스에서는 DBA가 키 또는 실제 키를 포함하는 키 저장소에 액세스할 수 없고, 보안 관리자가 중요한 데이터를 포함하는 데이터베이스에 액세스할 수 없습니다. 역할 구분을 사용하는 키 관리는 조직의 DBA가 중요한 데이터에 액세스할 수 없도록 하려는 경우에 권장됩니다. 

**참고:** 보안 관리자는 일반 텍스트 키를 생성하고 사용하므로 데이터베이스 시스템을 호스트하는 컴퓨터나 DBA 또는 악의적 사용자가 될 수 있는 다른 사용자가 액세스할 수 있는 컴퓨터에서 해당 태스크를 수행하면 안 됩니다. 

## <a name="managing-keys-without-role-separation"></a>역할 구분을 사용하지 않고 키 관리
상시 암호화 키가 역할 구분을 사용하지 않고 관리되는 경우 한 사람이 보안 관리자 및 DBA 역할을 모두 맡을 수 있으므로 해당 사용자가 키/키 저장소와 키 메타데이터를 둘 다 액세스하고 관리할 수 있어야 합니다. 역할 구분을 사용하지 않는 키 관리는 DevOps 모델을 사용하는 조직이나 데이터베이스가 클라우드에서 호스트되고 클라우드 관리자(온-프레미스 DBA 아님)가 중요한 데이터에 액세스할 수 없도록 제한하는 것이 주요 목표인 경우에 권장됩니다.



## <a name="tools-for-managing-always-encrypted-keys"></a>상시 암호화 키 관리 도구

상시 암호화 키는 [SSMS(SQL Server Management Studio)](https://msdn.microsoft.com/library/ms174173.aspx) 및 [PowerShell](../../scripting/sql-server-powershell.md)을 사용하여 관리할 수 있습니다.

- **SSMS(SQL Server Management Studio)** – 키 저장소 액세스 및 데이터베이스 액세스와 관련된 태스크를 결합하는 대화 상자와 마법사를 제공하므로 SSMS는 역할 구분을 지원하지 않지만 쉽게 키를 구성할 수 있게 합니다. SSMS를 사용하여 키를 관리하는 방법은 다음을 참조하세요.
    - [열 마스터 키 프로비전](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#provisioncmk)
    - [열 암호화 키 프로비전](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#provisioncek)
    - [열 마스터 키 순환](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#rotatecmk)
    - [열 암호화 키 순환](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#rotatecek)


- **SQL Server PowerShell** – 역할 구분을 사용 및 사용하지 않고 상시 암호화 키를 관리하기 위한 cmdlet이 포함되어 있습니다. 참조 항목:
    - [PowerShell을 사용하여 상시 암호화 키 구성](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
    - [PowerShell을 사용하여 상시 암호화 키 순환](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)


## <a name="SecurityForKeyManagement"></a> 키 관리에 대한 보안 고려 사항

상시 암호화의 주요 목표는 데이터베이스 시스템 또는 해당 호스팅 환경이 손상된 경우에도 데이터베이스에 저장된 중요한 데이터를 안전하게 보호하는 것입니다. 상시 암호화가 중요한 데이터 누출 방지에 도움이 되는 보안 공격의 예는 다음과 같습니다.

- DBA와 같은 높은 권한을 가진 악의적인 데이터베이스 사용자가 중요한 데이터 열을 쿼리하는 경우
- SQL Server 인스턴스를 호스트하는 컴퓨터의 악의적인 관리자가 메모리에서 SQL Server 프로세스 또는 SQL Server 프로세스 덤프 파일을 검색하는 경우
- 악의적인 데이터 센터 운영자가 고객 데이터베이스를 쿼리하거나 SQL Server 덤프 파일을 검사하거나 클라우드에서 고객 데이터를 호스트하는 컴퓨터의 메모리를 검사하는 경우
- 데이터베이스를 호스트하는 컴퓨터에서 실행되는 맬웨어

상시 암호화가 이러한 유형의 공격을 효과적으로 방지하려면 키 관리 프로세스에서 열 마스터 키와 열 암호화 키는 물론 열 마스터 키를 포함하는 키 저장소에 대한 자격 증명이 잠재적인 공격자에게 노출되지 않도록 해야 합니다. 다음 몇 가지 지침을 따라야 합니다.

- 데이터베이스를 호스트하는 컴퓨터에서 열 마스터 키 또는 열 암호화 키를 생성하지 않습니다. 대신, 키 관리에만 사용되거나 키에 액세스해야 하는 응용 프로그램을 호스트하는 컴퓨터인 별도 컴퓨터에서 키를 생성합니다. 즉, 상시 암호화 키를 프로비전하거나 유지 관리하는 데 사용되는 컴퓨터에 공격자가 액세스할 경우 키가 짧은 시간 동안만 도구의 메모리에 표시되는 경우에도 키를 얻을 수 있기 때문에 **데이터베이스를 호스트하는 컴퓨터에서 키를 생성하는 데 사용되는 도구를 실행하면 안 됩니다** .
- 키 관리 프로세스에서 열 마스터 키 또는 열 암호화 키가 실수로 공개되지 않도록 하려면 키 관리 프로세스를 정의 및 구현하기 전에 잠재적인 악의적 사용자와 보안 위협을 확인하는 것이 중요합니다. 예를 들어 DBA가 중요한 데이터에 액세스할 수 없게 하려는 경우 DBA는 키 생성을 담당할 수 없습니다. 그러나 메타데이터에는 일반 텍스트 키가 포함되지 않으므로 DBA가 데이터베이스의 키 메타데이터를 *관리할 수 있습니다* .

## <a name="next-steps"></a>Next Steps

- [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [PowerShell을 사용하여 상시 암호화 키 구성](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
- [PowerShell을 사용하여 상시 암호화 키 순환](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [SQL Server Management Studio를 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

## <a name="additional-resources"></a>추가 리소스

- [상시 암호화(데이터베이스 엔진)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted (Client Development)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [상시 암호화 마법사 자습서(Azure 주요 자격 증명 모음)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault/)
- [상시 암호화 마법사 자습서(Windows 인증서 저장소)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)





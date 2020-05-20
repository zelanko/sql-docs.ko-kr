---
title: DAC package로 Always Encrypted를 사용하여 열 암호화 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df18a2ca6f79982db41b5188283bf1721b518e31
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73595748"
---
# <a name="configure-column-encryption-using-always-encrypted-with-a-dac-package"></a>DAC package로 Always Encrypted를 사용하여 열 암호화 구성 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

DACPAC라고도 하는 [DAC(데이터 계층 애플리케이션) 패키지](../../data-tier-applications/data-tier-applications.md)는 테이블 및 테이블 내 열을 비롯한 모든 SQL Server 개체를 정의하는 SQL Server 데이터베이스 배포의 이식 가능한 단위입니다. DACPAC를 데이터베이스에 게시하는 경우(DACPAC를 사용하여 데이터베이스를 업그레이드하는 경우) DACPAC의 스키마와 일치하도록 대상 데이터베이스의 스키마가 업데이트를 가져옵니다. SQL Server Management Studio, [PowerShell](../../data-tier-applications/upgrade-a-data-tier-application.md#UpgradeDACPowerShell) 또는 [sqlpackage](../../../tools/sqlpackage.md#publish-parameters-properties-and-sqlcmd-variables)에서 [데이터 계층 애플리케이션 업그레이드 마법사](../../data-tier-applications/upgrade-a-data-tier-application.md#UsingDACUpgradeWizard)를 사용하여 DACPAC를 게시할 수 있습니다.

이 문서에서는 DACPAC 또는/및 대상 데이터베이스에 [Always Encrypted](always-encrypted-database-engine.md)로 보호되는 열이 포함된 경우 데이터베이스를 업그레이드할 때 특별히 고려해야 할 사항을 살펴봅니다. DACPAC에 있는 열의 암호화 체계가 대상 데이터베이스에 있는 기존 열의 암호화 체계와 다른 경우 DACPAC를 게시하면 열에 저장된 데이터가 암호화되거나, 암호 해독되거나 다시 암호화됩니다. 자세한 내용은 아래 표를 참조하세요.

| 조건|작업|
|:---|:---|
|DACPAC에서는 열이 암호화되고 데이터베이스에서는 암호화되지 않습니다.| 열의 데이터가 암호화됩니다.|
|DACPAC에서는 열이 암호화되지 않고 데이터베이스에서는 암호화됩니다.| 열의 데이터 암호가 해독됩니다(열에 대한 암호화가 제거됨).|
| DACPAC와 데이터베이스 둘 다에서 열이 암호화되지만 DACPAC의 열은 데이터베이스의 해당 열과 다른 암호화 유형 또는/및 다른 열 암호화 키를 사용합니다.|열의 데이터 암호가 해독된 다음 DACPAC의 암호화 구성에 맞게 다시 암호화됩니다.|

DAC 패키지를 배포하면 Always Encrypted에 사용되는 열 마스터 키 또는 열 암호화 키의 메타데이터 개체가 생성되거나 제거될 수도 있습니다.

## <a name="performance-considerations"></a>성능 고려 사항
암호화 작업을 수행하려면 DACPAC를 배포하는 데 사용하는 도구가 데이터베이스 외부로 데이터를 이동해야 합니다. 이 도구는 데이터베이스에서 원하는 암호화 구성을 사용하여 새 테이블을 만들고, 원래 테이블에서 모든 데이터를 로드하고, 요청된 암호화 작업을 수행하고, 데이터를 새 테이블에 업로드한 후 원래 테이블을 새 테이블로 바꿉니다. 암호화 작업을 실행하는 데 시간이 오래 걸릴 수 있습니다. 이 시간 동안에는 데이터베이스에서 트랜잭션을 쓸 수 없습니다. 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)]를 사용하고 SQL Server 인스턴스가 보안 Enclave로 구성된 경우 데이터베이스 외부로 데이터를 이동하지 않고도 바로 암호화 작업을 실행할 수 있습니다. [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)을 참조하세요. DACPAC 배포에는 바로 암호화를 사용할 수 없습니다.

::: moniker-end

## <a name="permissions-for-publishing-a-dac-package-if-always-encrypted-is-set-up"></a>Always Encrypted가 설정된 경우 DAC 패키지를 게시하는 데 필요한 사용 권한

DACPAC 또는/및 대상 데이터베이스에 Always Encrypted가 설정된 경우 DAC 패키지를 게시하려면 DACPAC의 스키마와 대상 데이터베이스 스키마 간 차이에 따라 아래 사용 권한 중 일부 또는 모두가 필요할 수 있습니다.

*ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*, *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

업그레이드 작업이 데이터 암호화 작업을 트리거하는 경우 영향을 받는 열에 대해 구성된 열 마스터 키에도 액세스할 수 있어야 합니다.

- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure Key Vault** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 *create*, *get*, *unwrapKey*, *wrapKey*, *sign* 및 *verify* 권한이 필요합니다.
- **CNG(키 저장소 공급 기업)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급 기업)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요. 

 
## <a name="next-steps"></a>다음 단계
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)
- [SQL Server Management Studio로 Always Encrypted를 사용하여 열 쿼리](always-encrypted-query-columns-ssms.md)

## <a name="see-also"></a>참고 항목  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Always Encrypted를 위한 키 관리 개요](overview-of-key-management-for-always-encrypted.md) 
 - [SQL Server Management Studio를 사용하여 Always Encrypted 구성](configure-always-encrypted-using-sql-server-management-studio.md)
 - [Always Encrypted 마법사를 사용하여 열 암호화 구성](always-encrypted-wizard.md)
 - [PowerShell로 Always Encrypted를 사용하여 열 암호화 구성](configure-column-encryption-using-powershell.md)
 

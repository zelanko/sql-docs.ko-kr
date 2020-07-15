---
title: Always Encrypted 마법사를 사용하여 열 암호화 구성 | Microsoft Docs
description: SQL Server에서 Always Encrypted 마법사를 사용하여 데이터베이스 열에 Always Encrypted 구성을 설정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql13.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords:
- Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f592004e96a9b469a56bc9ff85b8f4080af38406
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627450"
---
# <a name="configure-column-encryption-using-always-encrypted-wizard"></a>Always Encrypted 마법사를 사용하여 열 암호화 구성
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

Always Encrypted 마법사는 선택한 데이터베이스 열에 대해 원하는 [Always Encrypted](always-encrypted-database-engine.md) 구성을 설정할 수 있는 강력한 도구입니다. 현재 구성 및 원하는 대상 구성에 따라 마법사에서 열을 암호화하거나, 암호를 해독(암호화 제거)하거나, 다시 암호화(예: 열에 대해 구성된 현재 형식과 다른 암호화 형식 또는 새 열 암호화 키 사용)할 수 있습니다. 마법사를 한 번 실행하여 여러 열을 구성할 수 있습니다.

이 마법사를 사용하면 기존 열 암호화 키를 사용하여 열을 암호화하거나 새 열 암호화 키 또는 새 열 암호화 키와 새 열 마스터 키 모두를 생성하도록 선택할 수 있습니다. 

이 마법사는 데이터를 데이터베이스 외부로 이동하고 SSMS 프로세스 내에서 암호화 작업을 수행하는 방식으로 작동합니다. 마법사는 데이터베이스에서 원하는 암호화 구성을 사용하여 새 테이블을 만들고, 원래 테이블에서 모든 데이터를 로드하고, 요청된 암호화 작업을 수행하고, 데이터를 새 테이블에 업로드한 다음 원래 테이블을 새 테이블로 바꿉니다.

> [!NOTE]
> 암호화 작업을 실행하는 데 시간이 오래 걸릴 수 있습니다. 이 시간 동안에는 데이터베이스에서 트랜잭션을 쓸 수 없습니다. PowerShell은 보다 대규모의 테이블에 대한 암호화 작업에 권장되는 도구입니다. [PowerShell로 Always Encrypted를 사용하여 열 암호화 구성](configure-column-encryption-using-powershell.md)을 참조하세요.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)]를 사용하고 SQL Server 인스턴스가 보안 Enclave로 구성된 경우 데이터베이스 외부로 데이터를 이동하지 않고도 바로 암호화 작업을 실행할 수 있습니다. [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)을 참조하세요. 이 마법사는 내부 암호화를 지원하지 않습니다.

::: moniker-end

PowerShell을 사용하는 것이 좋습니다. 

 - 마법사를 사용하여 Always Encrypted를 구성하고 클라이언트 애플리케이션에서 사용하는 방법을 보여 주는 엔드투엔드 연습은 다음과 같은 Azure SQL Database 자습서를 참조하세요.
    - [Windows 인증서 저장소에서 Always Encrypted 및 열 마스터 키를 사용하여 Azure SQL Database의 중요한 데이터 보호](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)
    - [Azure Key Vault에서 Always Encrypted 및 열 마스터 키를 사용하여 Azure SQL Database의 중요한 데이터 보호](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault)

 - 마법사 사용이 포함된 비디오는 [상시 암호화를 사용하여 중요 데이터 보안 유지](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)를 참조하세요. 그리고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보안 팀 블로그 [SSMS 암호화 마법사 - 간단한 몇 단계로 상시 암호화 설정](https://techcommunity.microsoft.com/t5/SQL-Server/SSMS-Encryption-Wizard-Enabling-Always-Encrypted-in-a-Few-Easy/ba-p/384545)을 참조하세요.  
 - Always Encrypted 키에 대한 자세한 내용은 [Always Encrypted를 위한 키 관리 개요](overview-of-key-management-for-always-encrypted.md)를 참조하세요.
 - Always Encrypted에서 지원되는 암호화 유형에 대한 자세한 내용은 [결정적 암호화 또는 임의 암호화 선택](always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)을 참조하세요.
 
 ## <a name="permissions"></a>사용 권한
마법사를 사용하여 암호화 작업을 수행하려면 **VIEW ANY COLUMN MASTER KEY DEFINITION** 및 **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** 권한이 있어야 합니다. 또한 키를 보유하는 키 저장소에서 사용하는 열 마스터 키에 액세스할 수 있는 권한이 있어야 합니다.
- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure Key Vault** – 열 마스터 키를 포함하는 자격 증명 모음에 대한 get, unwrapKey 및 verify 권한이 필요합니다.
- **CNG(키 저장소 공급 기업)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급 기업)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 사용 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.

또한 마법사를 사용하여 새 키를 만드는 경우에는 [새 열 마스터 키 대화 상자를 사용하여 열 마스터 키 프로비전](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog) 및 [새 열 암호화 키 대화 상자를 사용하여 열 암호화 키 프로비전](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)에 나열된 추가 권한이 있어야 합니다.

## <a name="open-the-always-encrypted-wizard"></a>Always Encrypted 마법사 열기
다음 세 가지 수준에서 마법사를 시작할 수 있습니다. 
- 데이터베이스 수준 - 서로 다른 테이블에 있는 여러 열을 암호화하려는 경우
- 테이블 수준 - 동일한 테이블에 있는 여러 열을 암호화하려는 경우
- 열 수준 - 특정 열을 암호화하려는 경우
 
 1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 개체 탐색기 구성 요소를 사용하여 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에 연결합니다.  
   
 2. 암호화하려면 다음을 수행합니다.
     1. 데이터베이스의 서로 다른 테이블에 있는 여러 열은 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업**을 가리킨 다음 **열 암호화를** 선택합니다.
     1. 동일한 테이블에 있는 여러 열은 해당 테이블로 이동하여 마우스 오른쪽 단추로 클릭한 다음 **열 암호화**를 선택합니다.
     1. 개별 열은 해당 열로 이동하여 마우스 오른쪽 단추로 클릭한 다음 **열 암호화**를 선택합니다.


   
 ## <a name="column-selection-page"></a>열 선택 페이지
이 페이지에서는 암호화, 다시 암호화 또는 암호 해독하려는 열을 선택하고 선택한 열에 대한 대상 암호화 구성을 정의합니다.

일반 텍스트 열(암호화되지 않은 열)을 암호화하려면 암호화 유형(**결정적** 또는 **임의**) 및 열 암호화 키를 선택합니다. 

암호화 유형을 변경하거나 이미 암호화된 열에 대한 열 암호화 키를 순환(변경)하려면 원하는 암호화 유형 및 키를 선택합니다. 

마법사에서 새 열 암호화 키를 사용하여 하나 이상의 열을 암호화 또는 다시 암호화하게 하려면 이름에 **(신규)** 가 포함된 키를 선택합니다. 그러면 마법사에서 키를 생성합니다.

현재 암호화된 열의 암호를 해독하려면 암호화 형식에 **일반 텍스트**를 선택합니다.


> [!NOTE]
> 마법사에서는 임시 및 메모리 내 테이블에 대한 암호화 작업을 지원하지 않습니다. Transact-SQL을 사용하여 빈 임시 또는 메모리 내 테이블을 만들고 애플리케이션을 사용하여 데이터를 삽입할 수 있습니다.

## <a name="master-key-configuration-page"></a>마스터 키 구성 페이지
이전 페이지의 열에 대해 자동 생성된 열 암호화 키를 선택한 경우 이 페이지에서 기존 열 마스터 키를 선택하거나 열 암호화 키를 암호화하는 새 열 마스터 키를 구성해야 합니다. 

새 열 마스터 키를 구성할 때 Windows 인증서 저장소 또는 Azure Key Vault에서 기존 키를 선택하고 마법사에서 데이터베이스에 키에 대한 메타데이터 개체만 만들도록 하거나, 데이터베이스에 키와 해당 키를 설명하는 메타데이터를 모두 생성하도록 선택할 수 있습니다. 

Windows 인증서 저장소, Azure Key Vault 또는 다른 키 저장소에 열 마스터 키를 만들고 저장하는 방법에 대한 자세한 내용은 [Always Encrypted용 열 마스터 키 만들기 및 저장](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)을 참조하세요.

> [!TIP]
> 이 마법사를 사용하면 Windows 인증서 저장소 및 Azure Key Vault에서만 키를 찾아보고 만들 수 있습니다. 또한 새 키와 해당 키를 설명하는 데이터베이스 메타데이터 개체의 이름을 자동으로 생성합니다. 키 프로비전 방법에 대한 추가 제어 및 열 마스터 키를 포함하는 키 저장소에 대한 추가 선택 항목이 필요한 경우 먼저 **새 열 마스터 키** 및 **새 열 암호화 키** 대화 상자를 사용하여 키를 만든 다음, 마법사를 실행하고 만든 키를 선택할 수 있습니다. [새 열 마스터 키 대화 상자를 사용하여 열 마스터 키 프로비전](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog) 및 [새 열 암호화 키 대화 상자를 사용하여 열 암호화 키 프로비전](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)을 참조하세요. 

## <a name="next-steps"></a>다음 단계
- [SQL Server Management Studio로 Always Encrypted를 사용하여 열 쿼리](always-encrypted-query-columns-ssms.md)
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)

## <a name="see-also"></a>참고 항목  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Always Encrypted를 위한 키 관리 개요](overview-of-key-management-for-always-encrypted.md) 
 - [SQL Server Management Studio를 사용하여 Always Encrypted 구성](configure-always-encrypted-using-sql-server-management-studio.md)
 - [PowerShell을 사용하여 Always Encrypted 키 프로비저닝](configure-always-encrypted-keys-using-powershell.md)
 - [PowerShell로 Always Encrypted를 사용하여 열 암호화 구성](configure-column-encryption-using-powershell.md)
 - [DAC 패키지로 Always Encrypted를 사용하여 열 암호화 구성](configure-always-encrypted-using-dacpac.md)

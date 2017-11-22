---
title: "상시 암호화 마법사 | Microsoft 문서"
ms.custom: 
ms.date: 05/04/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords: Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8d07fe91f365bd274d835d77b22efb8830d09b70
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="always-encrypted-wizard"></a>상시 암호화 마법사
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

<a name="use-the-always-encrypted-wizard-to-help-protect-sensitive-data--stored-in-a-sql-server-database-always-encrypted-allows-clients-to-encrypt-sensitive-data-inside-client-applications-and-never-reveal-the-encryption-keys-to-sql-server-as-a-result-always-encrypted-provides-a-separation-between-those-who-own-the-data-and-can-view-it-and-those-who-manage-the-data-but-should-have-no-access--for-a-full-description-of-the-feature-see-always-encrypted-40database-engine41relational-databasessecurityencryptionalways-encrypted-database-enginemd"></a>**상시 암호화 마법사** 를 사용하여 SQL Server 데이터베이스에 저장된 중요 데이터를 보호할 수 있습니다. 상시 암호화를 사용하면 클라이언트가 클라이언트 응용 프로그램의 중요한 데이터를 암호화하고 암호화 키를 SQL Server에 표시하지 않을 수 있습니다. 따라서 상시 암호화는 데이터를 소유하고 볼 수 있는 사람과 데이터를 관리하지만 액세스 권한이 없어야 하는 사람을 분리합니다.  기능에 대한 자세한 내용은 [상시 암호화&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요.  
 -  
 - 마법사를 사용하여 상시 암호화를 구성하고 클라이언트 응용 프로그램에서 사용하는 방법을 보여 주는 종합 연습은 [SQL 데이터베이스 자습서: 상시 암호화로 중요한 데이터 보호](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)를 참조하세요.  
 -  
 - 마법사 사용이 포함된 비디오는 [상시 암호화를 사용하여 중요 데이터 보안 유지](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)를 참조하세요. 그리고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보안 팀 블로그 [SSMS 암호화 마법사 - 간단한 몇 단계로 상시 암호화 설정](http://blogs.msdn.com/b/sqlsecurity/archive/2015/11/01/ssms-encryption-wizard-enabling-always-encrypted-made-easy.aspx)을 참조하세요.  
 -  
 - **사용 권한:** 이 마법사를 사용하여 암호화된 열을 쿼리하고 키를 선택하려면 `VIEW ANY COLUMN MASTER KEY DEFINITION` 및 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 사용 권한이 있어야 합니다. 새 키를 만들려면 `ALTER ANY COLUMN MASTER KEY` 및 `ALTER ANY COLUMN ENCRYPTION KEY` 사용 권한이 있어야 합니다.  
 -  
 -#### Always Encrypted 마법사를 열려면  
 -  
 -1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 개체 탐색기 구성 요소를 사용하여 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에 연결합니다.  
 -  
 -2.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **열 암호화**를 클릭합니다.  
 -  
 -## 열 선택 영역 페이지  
 - 테이블과 열을 찾은 다음 선택한 열의 암호화 유형(결정적 또는 임의)과 암호화 키를 선택합니다. 현재 암호화된 열의 암호화를 해제하려면 **일반 텍스트**를 선택합니다. 열 암호화 키를 회전하려면 다른 암호화 키를 선택합니다. 그러면 마법사가 열의 암호화를 해제하고 새 키로 열을 다시 암호화합니다. ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 메모리 내 임시 테이블을 암호화할 수 있지만 이 마법사로 구성할 수는 없습니다.)  
 -  
 -## 마스터 키 구성 페이지  
 - Windows 인증서 저장소 또는 Azure 키 자격 증명 모음에 새 열 마스터 키를 만듭니다. 자세한 내용은 키 저장소 아래 링크를 참조하세요.  
 -  
 - 열 선택 페이지에서 자동 생성되는 열 암호화 키를 선택한 경우 생성된 열 암호화 키를 암호화할 때 적용할 열 마스터 키를 구성해야 합니다. 데이터베이스에 이미 열 마스터 키를 정의한 경우 해당 키를 선택할 수 있습니다. (기존 열 마스터 키를 사용하려면 사용자가 키에 대한 액세스 권한이 있어야 합니다.) 또는 선택한 열 저장소(Windows 인증서 저장소 또는 Azure 키 자격 증명 모음)에 열 마스터 키를 만들고 데이터베이스에서 키를 정의할 수 있습니다.  
 -  
 - **키 저장소**  
 -  
 - 열 마스터 키를 저장할 위치를 선택합니다.  
 -  
 --   **Windows 인증서에 마스터 키 저장** 자세한 내용은 [인증서 저장소 사용](https://msdn.microsoft.com/library/windows/desktop/aa388160.aspx)을 참조하세요.  
 -  
 --   **AKV에 마스터 키 저장** 자세한 내용은 [Azure Key Vault 시작하기](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)를 참조하세요.  
 -  
 - Azure 키 자격 증명 모음에 열 마스터 키를 생성하려면 사용자가 키 자격 증명 모음에 대해 **WrapKey**, **UnwrapKey**, **확인**, **서명** 권한이 있어야 합니다. 사용자는 **가져오기**, **목록**, **만들기**, **삭제**, **업데이트**, **가져오기**, **백업**, **복원** 권한이 필요할 수도 있습니다. 자세한 내용은 [Azure 주요 자격 증명 모음이란?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/) 및   [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx)를 참조하세요.  
 -  
 - 이 마법사는 두 가지 옵션만 지원합니다. 하드웨어 보안 모듈 및 고객 저장소는 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)]를 사용하여 구성해야 합니다.  
 -  
 -## Always Encrypted 용어  
 -  
 --   **결정적 암호화**는 지정된 일반 텍스트 값에 대해 항상 동일한 암호화된 값을 생성하는 방법을 사용합니다. 결정적 암호화를 사용하는 경우 암호화된 값을 기반으로 테이블 조인, 동등 여부 기준 필터링 및 그룹화가 가능하지만, 권한이 없는 사용자가 암호화된 열의 패턴을 검사하여 암호화된 값에 대한 정보를 추측할 수도 있습니다. 이 약점은 True/False 또는 North/South/East/West 지역과 같은 가능한 암호화된 값의 작은 집합이 있는 경우에 증가합니다. 결정적 암호화에서는 문자 열에 대해 binary2 정렬 순서를 적용하는 열 데이터 정렬을 사용해야 합니다.  
 -  
 --   **임의 암호화**는 예측하기 어려운 방식으로 데이터를 암호화하는 방법을 사용합니다. 임의 암호화는 더 안전하지만 암호화된 열에서 동등 검색, 그룹화, 인덱싱 및 조인을 금지합니다.  
 -  
 --   **열 마스터 키**는 열 암호화 키를 암호화하는 데 사용되는 키를 보호합니다. 열 마스터 키는 신뢰할 수 있는 키 저장소에 저장되어야 합니다. 열 마스터 키에 대한 정보는 해당 위치를 포함하여 시스템 카탈로그 뷰에서 데이터베이스에 저장됩니다.  
 -  
 --   **열 암호화 키**는 데이터베이스 열에 저장된 중요한 데이터를 암호화하는 데 사용됩니다. 열의 모든 값은 단일 열 암호화 키를 사용하여 암호화할 수 있습니다. 열 암호화 키의 암호화된 값은 시스템 카탈로그 뷰에서 데이터베이스에 저장됩니다. 백업을 위해 열 암호화 키를 안전한/신뢰할 수 있는 위치에 저장해야 합니다.  
 -  
 -## 참고 항목  
 - [상시 암호화&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [Azure Key Vault를 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  

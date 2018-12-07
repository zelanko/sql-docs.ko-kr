---
title: Azure Key Vault를 사용한 확장 가능 키 관리(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 07/22/2016
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
- EKM, with key vault
- TDE, EKM and key vault
- Key Management with key vault
- SQL Server Connector, about
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 9bb567ea41c87b895314abb8c3f7cedc4bbfbc7d
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391027"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Azure 키 자격 증명 모음(SQL Server)을 사용한 확장 가능 키 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure 주요 자격 증명 모음용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화를 사용하도록 설정하여 Azure 주요 자격 증명 모음 서비스를 [확장 가능 키 관리 &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md) 공급자로 활용함으로써 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 키를 보호합니다.  
  
 이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 설명합니다. 추가 정보는 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md), [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)및 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)에서 확인할 수 있습니다.  
  
##  <a name="Uses"></a> EKM(확장 가능 키 관리)의 정의 및 사용하는 이유  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 [TDE&#40;투명한 데이터 암호화&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md), [CLE](../../../t-sql/functions/cryptographic-functions-transact-sql.md)(열 수준 암호화) 및 [백업 암호화](../../../relational-databases/backup-restore/backup-encryption.md) 등 중요한 데이터를 보호하는 데 도움이 되는 여러 유형의 암호화를 제공합니다. 이러한 모든 암호화에서는 이 기존의 키 계층에서 데이터가 DEK(대칭 데이터 암호화 키)를 사용하여 암호화됩니다. 이 대칭 데이터 암호화 키는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 저장된 키의 계층 구조로 암호화하여 추가적으로 보호하게 됩니다. 이 모델 대신, 다른 모델로 EKM 공급자 모델이 있습니다. EKM 공급자 아키텍처를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 외부 암호화 공급자에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 외부에 저장된 비대칭 키를 사용하여 데이터 암호화 키를 보호합니다. 이 모델은 추가 보안 계층을 추가하고 키와 데이터의 관리를 구분합니다.  
   
 다음 이미지는 기존 서비스 관리 키 계층과 Azure 주요 자격 증명 모음 시스템을 비교합니다.  
  
 ![ekm-key-hierarchy-traditional](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-traditional.png "ekm-key-hierarchy-traditional")  
  
   
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 Azure 주요 자격 증명 모음 간 브리지 역할을 하므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 은(는) Azure 주요 자격 증명 모음 서비스의 확장성, 고성능 및 고가용성을 활용할 수 있습니다. 다음 이미지는 키 계층이 Azure 주요 자격 증명 모음 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커넥터를 사용하여 EKM 공급자 아키텍처에서 작동하는 방법을 보여 줍니다.  
  
  Azure 주요 자격 증명 모음은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Azure 가상 컴퓨터의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 설치와 함께 온-프레미스 서버용으로 사용할 수 있습니다. 키 자격 증명 모음 서비스에서는 더 높은 수준의 비대칭 암호화 키 보호를 위해 세부적인 제어 및 모니터링이 이루어지는 HSM(하드웨어 보안 모듈)을 사용할 수도 있습니다. 주요 자격 증명 모음에 대한 자세한 내용은 [Azure 주요 자격 증명 모음](https://go.microsoft.com/fwlink/?LinkId=521401)을 참조하세요.  
  
 다음 이미지에 키 자격 증명 모음을 사용한 EKM의 프로세스 흐름이 요약되어 있습니다. 이미지의 프로세스 단계 번호는 이미지에서 설명하는 설정 단계 번호와 일치하지 않습니다.  
  
 ![Azure Key Vault를 사용하는 SQL Server EKM](../../../relational-databases/security/encryption/media/ekm-using-azure-key-vault.png "SQL Server EKM using the Azure Key Vault")  

> [!NOTE]  
>  1.0.0.440 및 이전 버전은 대체되었으며 프로덕션 환경에서 더 이상 지원되지 않습니다. [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=45344)를 방문하고 "SQL Server 커넥터 업그레이드"의 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) 페이지에 있는 지침을 사용하여 1.0.1.0 또는 이후 버전으로 업그레이드하세요.
  
 다음 단계에 대해서는 [Azure 주요 자격 증명 모음을 사용한 확장 가능 키 관리 설정 단계](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)를 참조하세요.  
  
 사용 시나리오에 대해서는 [SQL 암호화 기능을 통해 SQL Server 커넥터 사용](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 커넥터 유지 관리 및 문제 해결](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  

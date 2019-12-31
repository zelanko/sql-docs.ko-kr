---
title: SQL Server 암호화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: f2aa6c25f8e8741308ff8f8b5df93cb2af67ad91
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957099"
---
# <a name="sql-server-encryption"></a>SQL Server 암호화
  암호화는 키 또는 암호를 사용하여 데이터를 난독 처리하는 프로세스입니다. 이 경우 해당하는 암호 해독 키 또는 암호가 없으면 데이터를 사용할 수 없게 됩니다. 암호화를 통해 액세스 제어 문제를 해결할 수는 없습니다. 그러나 암호화를 사용하면 액세스 제어가 무시되는 경우에도 데이터 손실을 제한하여 보안이 향상됩니다. 예를 들어 데이터베이스 호스트 컴퓨터가 잘못 구성되어 해커가 중요한 데이터를 얻는 경우 해당 정보가 암호화되어 있으면 해킹한 정보를 사용하지 못할 수도 있습니다.  
  
 연결, 데이터 및 저장 프로시저에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 암호화를 사용할 수 있습니다. 다음 표에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 암호화에 대한 자세한 정보를 제공합니다.  
  
> [!IMPORTANT]  
>  암호화가 보안을 유지해 주는 유용한 도구지만 모든 데이터나 연결에 대해 고려해야 하는 것은 아닙니다. 암호화 구현 여부를 결정할 때는 사용자가 데이터에 액세스하는 방법을 고려해야 합니다. 사용자가 공용 네트워크를 통해 데이터에 액세스할 경우 보안을 높이기 위한 데이터 암호화가 필요할 수도 있습니다. 그러나 모든 액세스가 보안 인트라넷 구성과 관련된 경우 암호화가 필요하지 않을 수도 있습니다. 암호화를 사용하려면 암호, 키 및 인증서에 대한 유지 관리 전략도 고려해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [암호화 계층](encryption-hierarchy.md)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 암호화 계층에 대한 정보입니다.  
  
 [암호화 알고리즘 선택](choose-an-encryption-algorithm.md)  
 효과적인 암호화 알고리즘을 선택하는 방법에 대한 정보입니다.  
  
 [투명한 데이터 암호화 &#40;TDE&#41;](transparent-data-encryption.md)  
 데이터를 명시적으로 암호화하는 방법에 대한 일반적인 정보입니다.  
  
 [SQL Server 및 데이터베이스 암호화 키 &#40;데이터베이스 엔진&#41;](sql-server-and-database-encryption-keys-database-engine.md)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 암호화 키에는 중요한 데이터를 보호하는 데 사용되는 퍼블릭 키, 프라이빗 키 및 대칭 키의 조합이 포함됩니다. 이 섹션에서는 암호화 키를 구현하고 관리하는 방법에 대해 설명합니다.  
  
## <a name="related-content"></a>관련 콘텐츠  
 [SQL Server 보안](../securing-sql-server.md)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 플랫폼에 보안을 설정하는 방법 및 사용자 및 보안 개체 작업을 수행하는 방법에 대한 개요입니다.  
  
 [Transact-sql&#41;&#40;암호화 함수](/sql/t-sql/functions/cryptographic-functions-transact-sql)  
 암호화 함수 구현 방법에 대한 정보입니다.  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
 데이터를 암호화하기 위해 암호를 사용하는 방법에 대한 정보입니다.  
  
 [ENCRYPTBYKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
 데이터를 암호화하기 위해 대칭 키를 사용하는 방법에 대한 정보입니다.  
  
 [ENCRYPTBYASYMKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
 데이터를 암호화하기 위해 비대칭 키를 사용하는 방법에 대한 정보입니다.  
  
 [ENCRYPTBYCERT &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbycert-transact-sql)  
 데이터를 암호화하기 위해 인증서를 사용하는 방법에 대한 정보입니다.  
  
## <a name="external-resources"></a>외부 리소스  
 [SQL Server 2005 보안에 대 한 10 단계](https://www.itprotoday.com/sql-server/10-steps-sql-server-2005-security)  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 보안에 대한 현재 정보입니다.  
  
## <a name="see-also"></a>참고 항목  
 [key_encryptions &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-key-encryptions-transact-sql)   
 [SQL Server 및 데이터베이스 암호화 키 &#40;데이터베이스 엔진&#41;](sql-server-and-database-encryption-keys-database-engine.md)   
 [Reporting Services 암호화 키 백업 및 복원](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  

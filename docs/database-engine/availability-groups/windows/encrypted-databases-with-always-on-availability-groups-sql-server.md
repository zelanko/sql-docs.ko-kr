---
title: 가용성 그룹에 암호화된 데이터베이스 추가
description: 암호화된(또는 최근에 암호 해독된) 데이터베이스를 Always On 가용성 그룹에 추가하는 단계입니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b5e86fe6a4f37e4ac21afb3a9aa72d80d48f3544
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000190"
---
# <a name="add-an-encrypted-database-to-an-always-on-availability-group"></a>Always On 가용성 그룹에 암호화된 데이터베이스 추가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]과 함께 현재 암호화되었거나 최근에 암호 해독된 데이터베이스 사용에 대한 정보가 포함되어 있습니다.  
  
 
##  <a name="Restrictions"></a> 제한 사항  
  
-   데이터가 암호화되었거나 심지어 DEK(데이터베이스 암호화 키)를 포함하는 경우 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 또는 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 를 사용하여 데이터베이스를 가용성 그룹에 추가할 수 없습니다. 암호화된 데이터베이스가 암호 해독된 경우라도 해당 로그 백업에는 암호화된 데이터가 포함될 수 있습니다. 이 경우 데이터베이스에서 전체 초기 데이터 동기화를 수행하면 작업이 실패할 수 있습니다. 로그 복원 작업에는 DEK(데이터베이스 암호화 키)에서 사용된 인증서가 필요한데 이 인증서를 사용할 수 없기 때문입니다.  
  
     마법사를 사용하여 암호 해독된 데이터베이스를 가용성 그룹에 추가하기에 적합하도록 만들려면  
  
    1.  주 데이터베이스의 로그 백업을 만듭니다.  
  
    2.  주 데이터베이스의 전체 데이터베이스 백업을 만듭니다.  
  
    3.  보조 복제본을 호스팅하는 서버 인스턴스에서 데이터베이스 백업을 복원합니다.  
  
    4.  주 데이터베이스에서 새 로그 백업을 만듭니다.  
  
    5.  보조 데이터베이스에서 이 로그 백업을 복원합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [투명한 데이터 암호화&#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  

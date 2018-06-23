---
title: AlwaysOn 가용성 그룹 (SQL Server)를 사용 하 여 데이터베이스 암호화 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 929206505ffb7aedf292f23e35cbed77ebe4cc20
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181641"
---
# <a name="encrypted-databases-with-alwayson-availability-groups-sql-server"></a>AlwaysOn 가용성 그룹이 있는 암호화된 데이터베이스(SQL Server)
  이 항목에는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]과 함께 현재 암호화되었거나 최근에 암호 해독된 데이터베이스 사용에 대한 정보가 포함되어 있습니다.  
  
 **항목 내용:**  
  
-   [제한 사항](#Restrictions)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="Restrictions"></a> 제한 사항  
  
-   데이터가 암호화되었거나 심지어 DEK(데이터베이스 암호화 키)를 포함하는 경우 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 또는 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 를 사용하여 데이터베이스를 가용성 그룹에 추가할 수 없습니다. 암호화된 데이터베이스가 암호 해독된 경우라도 해당 로그 백업에는 암호화된 데이터가 포함될 수 있습니다. 이 경우 데이터베이스에서 전체 초기 데이터 동기화를 수행하면 작업이 실패할 수 있습니다. 로그 복원 작업에는 DEK(데이터베이스 암호화 키)에서 사용된 인증서가 필요한데 이 인증서를 사용할 수 없기 때문입니다.  
  
     마법사를 사용하여 암호 해독된 데이터베이스를 가용성 그룹에 추가하기에 적합하도록 만들려면  
  
    1.  주 데이터베이스의 로그 백업을 만듭니다.  
  
    2.  주 데이터베이스의 전체 데이터베이스 백업을 만듭니다.  
  
    3.  보조 복제본을 호스팅하는 서버 인스턴스에서 데이터베이스 백업을 복원합니다.  
  
    4.  주 데이터베이스에서 새 로그 백업을 만듭니다.  
  
    5.  보조 데이터베이스에서 이 로그 백업을 복원합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [투명한 데이터 암호화&#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
---
title: 서비스 마스터 키 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server]
- service master key [SQL Server], about service master key
ms.assetid: 85f2095d-2590-4f59-8a29-7e100edd02bb
caps.latest.revision: 17
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: bf45a708f34ed5a22e733287e3ec240817e91a9b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286989"
---
# <a name="service-master-key"></a>인스턴스에서 해당 인스턴스를 위해 생성되는 SMK(
  서비스 마스터 키는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 암호화 계층의 루트이며 처음으로 다른 키를 암호화해야 할 때 자동으로 생성됩니다. 기본적으로 서비스 마스터 키는 Windows 데이터 보호 API 및 로컬 컴퓨터 키를 사용하여 암호화됩니다. 서비스 마스터 키는 이 키를 만든 Windows 서비스 계정이나 서비스 계정 이름 및 암호에 대한 액세스를 갖고 있는 보안 주체만 열 수 있습니다.  
  
 서비스 마스터 키를 다시 생성하거나 복원하는 과정에는 전체 암호화 계층을 해독하고 다시 암호화하는 작업이 포함됩니다. 키가 손상된 경우가 아니면 이 리소스 중심 작업을 사용량이 낮은 기간 동안에만 수행하도록 예약해야 합니다.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서는 AES 암호화 알고리즘을 사용하여 SMK(서비스 마스터 키) 및 DMK(데이터베이스 마스터 키)를 보호합니다. AES는 이전 버전에서 사용하는 3DES보다 최신 암호화 알고리즘입니다. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 인스턴스를 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]로 업그레이드한 후 SMK와 DMK를 다시 생성해야 마스터 키가 AES로 업그레이드됩니다. SMK를 다시 생성하는 방법은 [ALTER SERVICE MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql) 및 [ALTER MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql)를 참조하세요.  
  
## <a name="best-practice"></a>최선의 구현 방법  
 서비스 마스터 키를 백업하고 백업 복사본을 사이트 외부의 안전한 위치에 보관하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
 [BACKUP SERVICE MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-service-master-key-transact-sql)  
  
 [RESTORE SERVICE MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-service-master-key-transact-sql)  
  
 [ALTER SERVICE MASTER KEY&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [암호화 계층](encryption-hierarchy.md)  
  
  

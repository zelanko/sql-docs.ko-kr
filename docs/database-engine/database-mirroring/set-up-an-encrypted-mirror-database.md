---
title: "암호화된 미러 데이터베이스 설정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "암호화 [SQL Server], 데이터베이스 미러링"
  - "암호화 [SQL Server], 데이터베이스 미러링"
  - "데이터베이스 마스터 키 [SQL Server], 데이터베이스 미러링"
  - "미러 데이터베이스 [SQL Server]"
  - "데이터베이스 미러링 [SQL Server], 보안"
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
caps.latest.revision: 24
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 24
---
# 암호화된 미러 데이터베이스 설정
  미러 데이터베이스의 데이터베이스 마스터 키에 대한 자동 암호 해독을 사용하려면 마스터 키를 암호화하는 데 사용한 암호를 미러 서버 인스턴스에 제공해야 합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 이후 버전에는 암호를 전송하는 메커니즘이 포함됩니다. 데이터베이스 미러링을 시작하기 전에 **sp_control_dbmasterkey_password**를 사용하여 데이터베이스 마스터 키에 대한 자격 증명을 만드세요. 미러되는 모든 데이터베이스에 대해 이 프로세스를 반복해야 합니다. 자세한 내용은 [sp_control_dbmasterkey_password&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)를 참조하세요.  
  
> [!CAUTION]  
>  **sa** 및 기타 상위 권한 서버 보안 주체에서 액세스하지 않아야 하는 데이터베이스에 대한 장애 조치(Failover) 암호 해독은 설정하지 마십시오. 서비스 마스터 키로 키 계층을 해독할 수 없도록 데이터베이스를 구성할 수 있습니다. 이 옵션은 **sa** 또는 기타 상위 권한 서버 보안 주체에서 액세스하지 않아야 하는 정보가 포함된 데이터베이스를 위한 심층 방어로 지원됩니다. 이러한 데이터베이스에 대해 장애 조치(failover) 암호 해독을 설정하면 이러한 심층 방어가 제거되어 **sa** 및 기타 상위 권한 서버 보안 주체에서 데이터베이스를 암호 해독할 수 있습니다.  
  
## 참고 항목  
 [sp_control_dbmasterkey_password&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
  
  
---
title: 데이터베이스 마스터 키 복원 | Microsoft 문서
description: SQL Server Management Studio를 Transact-SQL과 함께 사용하여 SQL Server에서 데이터베이스 마스터 키를 복원하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], importing
ms.assetid: 16897cc5-db8f-43bb-a38e-6855c82647cf
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 9860b952751937b18ca5e95e92ac959bb86abd23
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892241"
---
# <a name="restore-a-database-master-key"></a>데이터베이스 마스터 키 복원
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 데이터베이스 마스터 키를 복원하는 방법에 대해 설명합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="limitations-and-restrictions"></a>제한 사항  
  
- 마스터 키가 복원되면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 현재 사용 중인 마스터 키로 암호화된 모든 키의 암호를 해독한 다음 복원된 마스터 키를 사용하여 이러한 키를 암호화합니다. 이 리소스를 많이 사용하는 작업은 사용량이 낮은 기간 동안에만 수행하도록 예약해야 합니다. 현재 데이터베이스 마스터 키가 열려 있지 않거나 열 수 없는 경우 또는 이 키를 사용하여 암호화된 일부 키의 암호를 해독할 수 없는 경우 복원 작업이 실패합니다.  
  
- 암호 해독 중 하나가 실패하면 복원이 실패합니다. 오류를 무시하기 위해 FORCE 옵션을 사용할 수 있지만 이 옵션을 사용하면 암호를 해독할 수 없는 데이터를 손실할 수 있습니다.  
  
- 서비스 마스터 키로 마스터 키가 암호화된 경우 복원된 마스터 키는 서비스 마스터 키로도 암호화할 수 있습니다.  
  
- 현재 데이터베이스에 마스터 키가 없는 경우 RESTORE MASTER KEY가 마스터 키를 만듭니다. 새 마스터 키는 서비스 마스터 키로 자동으로 암호화되지 않습니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한
데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="using-sql-server-management-studio-with-transact-sql"></a>Transact-SQL과 함께 SQL Server Management Studio 사용  
  
### <a name="to-restore-the-database-master-key"></a>데이터베이스 마스터 키를 복원하려면  
  
1. 물리적 백업 미디어 또는 로컬 파일 시스템의 디렉터리에서 백업한 데이터베이스 마스터 키의 복사본을 검색합니다.  
  
2. **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
3. 표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
4. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  

    ```sql
    -- Restores the database master key of the AdventureWorks2012 database.  
    USE AdventureWorks2012;  
    GO  
    RESTORE MASTER KEY   
        FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
        ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
    GO  
    ```  
  
    > [!NOTE]  
    > 키의 경로와 암호(있는 경우)는 위에 나타난 것과 다릅니다. 둘 다 서버 및 키 설정에 대해 고유한지 확인하세요.  
  
 자세한 내용은 [RESTORE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/restore-master-key-transact-sql.md)를 참조하세요.  

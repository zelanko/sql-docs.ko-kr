---
title: SQL Server 변경 데이터베이스 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 255cc9373e18fc33ce1f43dd3be760e283d1e891
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438750"
---
# <a name="create-the-sql-server-change-database"></a>SQL Server 변경 데이터베이스 만들기
  새 인스턴스 마법사를 시작하면 CDC 데이터베이스 만들기 페이지가 열립니다. CDC 데이터베이스 만들기 페이지를 사용하여 새 CDC 인스턴스에 대한 정보를 제공하고 변경 데이터베이스를 새로 만들 수 있습니다.  
  
 새로 만든 CDC 데이터베이스는 SQL Server CDC에 사용할 수 있도록 설정되며 이를 위해서는 `sysadmin` 고정 서버 역할의 멤버인 로그인이 필요합니다.  
  
 Oracle CDC 인스턴스 만들기 마법사를 시작하는 사용자가 `sysadmin` 고정 서버 역할의 멤버가 아닌 경우 SQL Server에 연결 대화 상자가 열리고 SQL Server CDC에 데이터베이스 사용 태스크를 수행하기 위한 sysadmin 역할의 멤버 자격 증명을 요청합니다. CDC 데이터베이스가 만들어지면 `sysadmin` 로그인은 삭제되고 Oracle Designer 콘솔 시작 시 사용된 원래 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 작업이 다시 시작됩니다.  
  
> [!IMPORTANT]  
>  SQL Server CDC에 데이터베이스 사용 이외의 태스크의 경우 새 인스턴스 마법사를 실행하는 데 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 MSXDBCDC 데이터베이스에 대한 `dbcreator` 고정 서버 역할과 UPDATE 권한이 있어야 합니다.  
  
 SQL 서버에 연결 대화 상자에서 데이터를 입력하는 방법은 [SQL Server Connection for Instance Creation](sql-server-connection-for-instance-creation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **Oracle CDC 인스턴스**  
 만들려는 CDC 인스턴스에 대한 다음 정보를 입력합니다.  
  
-   **이름**: 새 서비스의 이름을 입력합니다. 이 이름은 새 변경 데이터베이스의 이름이기도 합니다.  
  
-   **설명**: 새 인스턴스를 식별하는 데 도움이 되는 설명을 입력합니다. 이 구성 요소는 선택 사항입니다.  
  
 **SQL Server 변경 데이터베이스**  
 이 섹션은 데이터베이스를 만드는 데 사용됩니다.  
  
1.  **변경 데이터베이스**: 이 이름은 새 변경 데이터베이스의 이름이기도 합니다. 데이터베이스의 이름은 인스턴스에 대해 지정한 이름과 동일합니다. 이 읽기 전용 필드에는 데이터베이스의 전체 경로가 표시됩니다.  
  
2.  **데이터베이스 만들기**: **데이터베이스 만들기** 를 클릭하여 데이터베이스를 만들 수 있습니다.  
  
     데이터베이스를 만들려면 로그인에 `sysasmin` 서버 역할이 있어야 합니다. 자세한 내용은 위의 보안 참고 사항을 참조하십시오.  
  
     데이터베이스를 만든 후 **다음** 을 클릭하여 [Connect to an Oracle Source Database](connect-to-an-oracle-source-database.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 변경 데이터베이스 인스턴스를 만드는 방법](how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle CDC Service](the-oracle-cdc-service.md)  
  
  

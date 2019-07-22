---
title: 서버 데이터 정렬 설정 또는 변경 | Microsoft 문서
ms.custom: ''
ms.date: 01/22/2019
ms.prod: sql
ms.reviewer: carlrab
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 81a776a0bece59f98042fec6cbf7b191ec82be1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140842"
---
# <a name="set-or-change-the-server-collation"></a>서버 데이터 정렬 설정 또는 변경

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  서버 데이터 정렬은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 설치된 모든 시스템 데이터베이스와 새로 만든 사용자 데이터베이스의 기본 데이터 정렬로 적용됩니다. 다음과 같은 영향을 주므로 신중하게 서버 수준 데이터 정렬을 선택해야 합니다.
 - `=`, `JOIN`, `ORDER BY` 및 텍스트 데이터를 비교하는 기타 연산자의 정렬 및 비교 규칙입니다.
 - 시스템 보기, 시스템 함수 및 TempDB의 개체에 있는 `CHAR`, `VARCHAR`, `NCHAR` 및 `NVARCHAR` 열의 데이터 정렬입니다(예: 임시 테이블).
 - 변수, 커서 및 `GOTO` 레이블의 이름입니다. 변수 @pi 및 @PI는 서버 수준 데이터 정렬에서 대/소문자를 구분하면 다른 변수로 간주되고, 서버 수준 데이터 정렬에서 대/소문자를 구분하지 않으면 동일한 변수로 간주됩니다.
  
## <a name="setting-the-server-collation-in-sql-server"></a>SQL Server에서 서버 데이터 정렬 설정

  서버 데이터 정렬은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 과정에서 지정됩니다. 기본 서버 수준 데이터 정렬은 **SQL_Latin1_General_CP1_CI_AS**입니다. 유니코드 전용 데이터 정렬은 서버 수준 데이터 정렬로 지정할 수 없습니다. 자세한 내용은 [Collation and Unicode Support](collation-and-unicode-support.md)을 참조하세요.
  
## <a name="changing-the-server-collation-in-sql-server"></a>SQL Server에서 서버 데이터 정렬 변경

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 데이터 정렬을 변경하는 작업은 복잡할 수 있으며 다음과 같은 단계가 포함됩니다.  
  
- 사용자 데이터베이스와 그 안의 모든 개체를 다시 만드는 데 필요한 정보나 스크립트가 모두 있는지 확인합니다.  
  
- [bcp Utility](../../tools/bcp-utility.md)등의 도구를 사용하여 모든 데이터를 내보냅니다. 자세한 내용은 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)를 참조하세요.  
  
- 모든 사용자 데이터베이스를 삭제합니다.  
  
- **setup** 명령의 SQLCOLLATION 속성에 새 데이터 정렬을 지정하여 master 데이터베이스를 다시 작성합니다. 예를 들어  
  
    ```sql  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]
    /SQLCOLLATION=CollationName  
    ```  
  
     자세한 내용은 [시스템 데이터베이스 다시 작성](../../relational-databases/databases/rebuild-system-databases.md)을 참조하세요.  
  
- 모든 데이터베이스와 그 안의 모든 개체를 만듭니다.  
  
- 모든 데이터를 가져옵니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 기본 데이터 정렬을 변경하는 대신 사용자가 만드는 각각의 새 데이터베이스에 대해 기본 데이터 정렬을 지정할 수 있습니다.  
  
## <a name="setting-the-server-collation-in-managed-instance"></a>Managed Instance에서 서버 데이터 정렬 설정

Azure SQL Managed Instance의 서버 수준 데이터 정렬은 인스턴스가 생성될 때 지정될 수 있고 나중에 변경될 수 없습니다. 인스턴스를 만드는 동안 [Azure Portal](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started#create-a-managed-instance) 또는 [PowerShell 및 Resource Manager 템플릿](https://docs.microsoft.com/azure/sql-database/scripts/sql-managed-instance-create-powershell-azure-resource-manager-template)을 통해 서버 수준 데이터 정렬을 설정할 수 있습니다. 기본 서버 수준 데이터 정렬은 **SQL_Latin1_General_CP1_CI_AS**입니다. 유니코드 전용 및 새 UTF-8 데이터 정렬은 서버 수준 데이터 정렬로 지정할 수 없습니다.
데이터베이스를 SQL Server에서 Managed Instance로 마이그레이션하는 경우 `SERVERPROPERTY(N'Collation')` 함수를 사용하여 원본 SQL Server에서 서버 데이터 정렬을 확인하고 SQL Server의 데이터 정렬과 일치하는 Managed Instance를 만듭니다. 일치하지 않는 서버 수준 데이터 정렬을 사용하여 SQL Server에서 Managed Instance로 데이터베이스를 마이그레이션하면 쿼리에서 몇 가지 예기치 않은 오류가 발생할 수 있습니다. 기존 Managed Instance에서 서버 수준 데이터 정렬을 변경할 수 없습니다.

## <a name="see-also"></a>참고 항목

 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)   
 [데이터베이스 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [열 데이터 정렬 설정 또는 변경](../../relational-databases/collations/set-or-change-the-column-collation.md)   
 [시스템 데이터베이스 다시 작성](../../relational-databases/databases/rebuild-system-databases.md)  
 

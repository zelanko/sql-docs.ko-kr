---
title: 백업 관리 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle Backup Management
- SQL Server Backup Management
ms.assetid: a1a03ef9-b6e8-4127-bad0-eae261251472
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: a11948b901e0f687b1daf537faa7b836c4618206
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68262967"
---
# <a name="managing-backups-oracletosql"></a>백업 관리(OracleToSQL)
Oracle 백업 관리를 사용 하면 테스트를 실행 하기 전이나 후에 테이블 데이터를 백업 및 복원할 수 있습니다. 백업 콘텐츠 관리 대화 상자를 사용 하 여 백업 콘텐츠를 관리할 수도 있습니다.  
  
## <a name="oracle-backup-management"></a>Oracle 백업 관리  
  
### <a name="backup"></a>Backup  
백업 대화 상자를 열려면 테스터 메뉴에서 Oracle Backup 관리를 가리키고 백업 ...을 클릭 합니다. 백업 대화 상자에 로드 된 Oracle 스키마의 모든 테이블을 표시 하는 Oracle 메타 데이터 트리가 표시 됩니다. 하나 이상의 테이블을 선택 하 여 백업을 수행 합니다.  
  
대화 상자에서 사용할 수 있는 단추는 다음과 같습니다.  
  
-   **상태 확인** 단추를 클릭 하 여 테이블의 백업 상태를 확인 합니다.  
  
-   테이블의 데이터를 백업 하려면 **백업** 단추를 클릭 합니다.  
  
-   **취소** 단추를 클릭 하 여 대화 상자를 닫습니다.  
  
### <a name="restore"></a>복원  
복원 대화 상자를 열려면 테스터 메뉴에서 Oracle Backup Management를 가리킨 다음 복원 ...을 클릭 합니다. 여기서는 백업에서 사용할 수 있는 테이블을 포함 하는 트리를 찾을 수 있습니다. 데이터를 복원 하려면 하나 이상의 테이블을 선택 합니다.  
  
대화 상자에서 사용할 수 있는 단추는 다음과 같습니다.  
  
-   **상태 확인** 단추를 클릭 하 여 테이블의 백업 상태를 확인 합니다.  
  
-   **복원** 단추를 클릭 하 여 백업 데이터를 테이블에 복원 합니다.  
  
-   **취소** 단추를 클릭 하 여 대화 상자를 닫습니다.  
  
### <a name="managing-backup-contents"></a>백업 콘텐츠 관리  
백업 콘텐츠 관리를 열려면 테스터 메뉴에서 Oracle Backup Management를 가리킨 다음 백업 콘텐츠 ...를 클릭 합니다. 여기서는 백업에서 테이블이 포함 된 트리를 찾을 수 있습니다.  
  
대화 상자에서 사용할 수 있는 단추는 다음과 같습니다.  
  
-   **상태 확인** 단추를 클릭 하 여 테이블의 백업 상태를 확인 합니다.  
  
-   백업에서 테이블을 제거 하려면 **제거** 단추를 클릭 합니다.  
  
-   **닫기** 단추를 클릭 하 여 대화 상자를 닫습니다.  
  
## <a name="sql-server-backup-management"></a>SQL Server 백업 관리  
SQL Server 백업 관리를 사용 하면 테스트를 실행 하기 전이나 후에 테이블 데이터를 백업 및 복원할 수 있습니다. 백업 콘텐츠 관리 대화 상자를 사용 하 여 백업 콘텐츠를 관리할 수도 있습니다.  
  
### <a name="backup"></a>Backup  
백업 대화 상자를 열려면 테스터 메뉴에서 백업 관리 SQL Server 가리킨 다음 백업 ...을 클릭 합니다. 백업 대화 상자에서 로드 된 SQL Server 데이터베이스의 모든 테이블을 표시 하는 SQL Server 메타 데이터 트리를 찾을 수 있습니다. 하나 이상의 테이블을 선택 하 여 백업을 수행 합니다.  
  
대화 상자에서 사용할 수 있는 단추는 다음과 같습니다.  
  
-   **상태 확인** 단추를 클릭 하 여 테이블의 백업 상태를 확인 합니다.  
  
-   **백업** 단추를 클릭 하 여 테이블의 데이터를 백업 합니다.  
  
-   **취소** 단추를 클릭 하 여 대화 상자를 닫습니다.  
  
### <a name="restore"></a>복원  
복원 대화 상자를 열려면 테스터 메뉴에서 백업 관리 SQL Server 가리킨 다음 복원 ...을 클릭 합니다. 여기서는 백업에서 사용할 수 있는 테이블을 포함 하는 트리를 찾을 수 있습니다. 데이터를 복원 하려면 하나 이상의 테이블을 선택 합니다.  
  
대화 상자에서 사용할 수 있는 단추는 다음과 같습니다.  
  
-   **상태 확인** 단추를 클릭 하 여 테이블의 백업 상태를 확인 합니다.  
  
-   **복원** 단추를 클릭 하 여 백업 데이터를 테이블에 복원 합니다.  
  
-   **취소** 단추를 클릭 하 여 대화 상자를 닫습니다.  
  
### <a name="managing-backup-contents"></a>백업 콘텐츠 관리  
백업 콘텐츠 관리를 열려면 테스터 메뉴에서 백업 관리 SQL Server 가리킨 다음 백업 콘텐츠 ...를 클릭 합니다. 여기서는 백업에서 테이블이 포함 된 트리를 찾을 수 있습니다.  
  
대화 상자에서 사용할 수 있는 단추는 다음과 같습니다.  
  
-   **상태 확인** 단추를 클릭 하 여 테이블의 백업 상태를 확인 합니다.  
  
-   백업에서 테이블을 제거 하려면 **제거** 단추를 클릭 합니다.  
  
-   **닫기** 단추를 클릭 하 여 대화 상자를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
[OracleToSQL&#41;&#40;마이그레이션된 데이터베이스 개체 테스트](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

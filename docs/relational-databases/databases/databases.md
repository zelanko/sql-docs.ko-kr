---
title: "데이터베이스 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data warehouse [SQL Server]
- OLTP databases [SQL Server]
- databases [SQL Server], about databases
ms.assetid: 316eea58-81b8-4bf3-a1fc-801946740e94
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 05f9976284e6207a1057f1b7308e7276d833daae
ms.lasthandoff: 04/11/2017

---
# <a name="databases"></a>데이터베이스
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 데이터베이스는 구조화된 데이터의 특정 집합이 저장되는 테이블 모음으로 구성됩니다. 테이블에는 행과 열의 모음이 들어 있습니다. 행은 레코드나 튜플이라고도 하고 열은 특성이라고도 합니다. 테이블의 각 열에는 날짜, 이름, 달러 금액 및 숫자와 같은 특정 유형의 정보가 저장됩니다.  
  
## <a name="basic-information-about-databases"></a>데이터베이스에 대한 기본 정보  
 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스가 하나 이상 설치될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 각 인스턴스는 하나 이상의 데이터베이스를 포함할 수 있습니다.  데이터베이스 내에 스키마라는 하나 이상의 개체 소유권 그룹이 있습니다. 각 스키마에는 테이블, 뷰, 저장 프로시저와 같은 데이터베이스 개체가 있습니다. 인증서 및 비대칭 키와 같은 일부 개체는 데이터베이스에는 포함되지만 스키마에는 포함되지 않습니다. 테이블을 만드는 방법은 [Tables](../../relational-databases/tables/tables.md)을 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스는 파일 시스템에 파일로 저장됩니다. 파일을 파일 그룹으로 그룹화할 수 있습니다. 파일 및 파일 그룹에 대한 자세한 내용은 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하십시오.  
  
 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 액세스하면 로그인으로 식별됩니다. 데이터베이스에 액세스하면 데이터베이스 사용자로 식별됩니다. 데이터베이스 사용자는 로그인을 기반으로 할 수 있습니다. 포함된 데이터베이스를 사용하도록 설정한 경우 로그인을 기반으로 하지 않는 데이터베이스 사용자를 만들 수 있습니다. 사용자에 대한 자세한 내용은 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)를 참조하세요.  
  
 데이터베이스에 대한 액세스 권한이 있는 사용자는 데이터베이스의 개체에 액세스할 수 있습니다. 개별 사용자에게 사용 권한을 부여할 수 있지만 데이터베이스 역할을 만들고 데이터베이스 사용자를 역할에 추가한 다음 해당 역할에 액세스 권한을 부여하는 것이 좋습니다. 사용자 대신 역할에 사용 권한을 부여하면 사용 권한을 일관적으로 유지하고 사용자 수의 증가와 지속적인 변화를 쉽게 파악할 수 있습니다. 역할 사용 권한에 대한 자세한 내용은 [CREATE ROLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md) 및 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)를 참조하세요.  
  
## <a name="working-with-databases"></a>데이터베이스 작업  
 데이터베이스를 사용하는 대부분의 사용자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 도구를 사용합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 도구에는 데이터베이스와 데이터베이스 내의 개체를 만드는 데 필요한 그래픽 사용자 인터페이스가 있습니다. 또한 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 작성하여 데이터베이스와 상호 작용하기 위한 쿼리 편집기가 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 디스크에서 설치하거나 MSDN에서 다운로드할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|||  
|-|-|  
|[시스템 데이터베이스](../../relational-databases/databases/system-databases.md)|[데이터베이스에서 데이터 또는 로그 파일 삭제](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)|  
|[포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)|[데이터베이스의 데이터 및 로그 공간 정보 표시](../../relational-databases/databases/display-data-and-log-space-information-for-a-database.md)|  
|[Microsoft Azure의 SQL Server 데이터 파일](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)|[데이터베이스의 크기 늘리기](../../relational-databases/databases/increase-the-size-of-a-database.md)|  
|[데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)|[데이터베이스 이름 바꾸기](../../relational-databases/databases/rename-a-database.md)|  
|[데이터베이스 상태](../../relational-databases/databases/database-states.md)|[단일 사용자 모드로 데이터베이스 설정](../../relational-databases/databases/set-a-database-to-single-user-mode.md)|  
|[파일 상태](../../relational-databases/databases/file-states.md)|[데이터베이스 축소](../../relational-databases/databases/shrink-a-database.md)|  
|[데이터베이스 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-database.md)|[파일 축소](../../relational-databases/databases/shrink-a-file.md)|  
|[데이터베이스를 다른 서버로 복사](../../relational-databases/databases/copy-databases-to-other-servers.md)|[데이터베이스의 속성 보기 또는 변경](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)|  
|[데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)|[SQL Server 인스턴스에서 데이터베이스의 목록 보기](../../relational-databases/databases/view-a-list-of-databases-on-an-instance-of-sql-server.md)|  
|[데이터베이스에 데이터 또는 로그 파일 추가](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)|[데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)|  
|[데이터베이스 메일의 구성 설정 변경](../../relational-databases/databases/change-the-configuration-settings-for-a-database.md)|[유지 관리 계획 마법사 사용](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|[데이터베이스 만들기](../../relational-databases/databases/create-a-database.md)|[사용자 정의 데이터 형식 별칭 만들기](../../relational-databases/databases/create-a-user-defined-data-type-alias.md)|  
|[데이터베이스 삭제](../../relational-databases/databases/delete-a-database.md)|[데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)|  
  
## <a name="related-content"></a>관련 내용  
 [인덱스](../../relational-databases/indexes/indexes.md)  
  
 [뷰](../../relational-databases/views/views.md)  
  
 [저장 프로시저&#40;데이터베이스 엔진&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  

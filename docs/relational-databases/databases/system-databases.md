---
description: 시스템 데이터베이스
title: 시스템 데이터베이스 | Microsoft 문서
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server]
- displaying system database data
- modifying system data
- viewing system database data
ms.assetid: 30468a7c-4225-4d35-aa4a-ffa7da4f1282
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3476e6d03afae3083e80a7fc607bff77922921b3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478334"
---
# <a name="system-databases"></a>시스템 데이터베이스

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 포함된 시스템 데이터베이스는 다음과 같습니다.  
  
|시스템 데이터베이스|Description|  
|---------------------|-----------------|  
|[master 데이터베이스](../../relational-databases/databases/master-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 모든 시스템 수준 정보를 기록합니다.|  
|[msdb 데이터베이스](../../relational-databases/databases/msdb-database.md)|SQL Server 에이전트에서 알림과 작업을 예약하는 데 사용됩니다.|  
|[model 데이터베이스](../../relational-databases/databases/model-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성되는 모든 데이터베이스에 대한 템플릿으로 사용됩니다. **model** 데이터베이스의 크기, 정렬, 복구 모델 또는 데이터베이스 옵션의 수정 내용은 이후에 생성되는 모든 데이터베이스에 적용됩니다.|  
|[Resource 데이터베이스](../../relational-databases/databases/resource-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함된 시스템 개체가 들어 있는 읽기 전용 데이터베이스입니다. 시스템 개체는 실제로는 **Resource** 데이터베이스에 저장되지만 논리적으로는 모든 데이터베이스의 **sys** 스키마에 나타납니다.|  
|[tempdb 데이터베이스](../../relational-databases/databases/tempdb-database.md)|임시 개체나 중간 결과 집합을 보관하기 위한 작업 영역입니다.|  

> [!IMPORTANT]
> Azure SQL Database 단일 데이터베이스와 탄력적 풀의 경우 master 데이터베이스 및 tempdb 데이터베이스만 적용됩니다. 자세한 내용은 [Azure SQL Database 서버란?](/azure/sql-database/sql-database-servers#what-is-an-azure-sql-database-server)을 참조하세요. Azure SQL Database의 컨텍스트에서 tempdb의 설명은 [Azure SQL Database의 tempdb 데이터베이스](tempdb-database.md#tempdb-database-in-sql-database)를 참조하세요. Azure SQL Managed Instance의 경우 모든 시스템 데이터베이스가 적용됩니다. Azure SQL Database Managed Instance에 대한 자세한 내용은 [Managed Instance란?](/azure/sql-database/sql-database-managed-instance)을 참조하세요.
  
## <a name="modifying-system-data"></a>시스템 데이터 수정  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 사용자가 시스템 테이블, 시스템 저장 프로시저 및 카탈로그 뷰와 같은 시스템 개체의 정보를 직접 업데이트할 수 없습니다. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 사용자가 시스템을 완전히 관리하고 데이터베이스의 모든 사용자와 개체를 관리하는 데 사용할 수 있는 완전한 관리 도구 집합을 제공합니다. 여기에는 다음과 같은 옵션이 포함됩니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]등의 관리 유틸리티  
  
-   SQL-SMO API. 이 도구를 통해 프로그래머는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 관리할 수 있는 완전한 기능을 애플리케이션에 포함할 수 있습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 및 저장 프로시저. 시스템 저장 프로시저와 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 문을 사용할 수 있습니다.  
  
 이러한 관리 도구는 시스템 개체의 변경 내용으로부터 애플리케이션을 보호합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 새 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 새로 추가되는 기능을 지원하기 위해 시스템 테이블을 변경해야 하는 경우가 있습니다. 시스템 테이블을 직접 참조하는 SELECT 문을 실행하는 애플리케이션은 대개 시스템 테이블의 이전 형식을 기준으로 합니다. 사이트는 시스템 테이블에서 선택되는 애플리케이션을 다시 작성해야만 새 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 업그레이드할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 시스템 저장 프로시저, DDL 및 SQL-SMO 게시 인터페이스를 고려하며 이러한 인터페이스와 이전 버전과의 호환성을 유지합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 시스템의 작업을 수정할 수 있기 때문에 시스템 테이블에 정의된 트리거는 지원하지 않습니다.  
  
> [!NOTE]  
>  시스템 데이터베이스는 UNC 공유 디렉터리에 있을 수 없습니다.  
  
## <a name="viewing-system-database-data"></a>시스템 데이터베이스 데이터 보기  
 애플리케이션에 필요한 정보를 얻기 위해 불가피한 경우가 아니면 시스템 테이블을 직접 쿼리하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 작성하지 마십시오. 대신 다음 항목을 사용하여 애플리케이션에서 카탈로그나 시스템 정보를 얻어야 합니다.  
  
-   시스템 카탈로그 뷰  
  
-   SQL-SMO  
  
-   WMI(Windows Management Instrumentation) 인터페이스  
  
-   ADO, OLE DB, ODBC 등의 애플리케이션에 사용되는 데이터 API의 카탈로그 함수, 메서드, 특성 또는 속성  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저 및 기본 제공 함수  
  
## <a name="related-tasks"></a>관련 작업  
 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [개체 탐색기에서 시스템 개체 숨기기](../../ssms/object/hide-system-objects-in-object-explorer.md)  
  
## <a name="related-content"></a>관련 내용  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
 [데이터베이스](../../relational-databases/databases/databases.md)  
  

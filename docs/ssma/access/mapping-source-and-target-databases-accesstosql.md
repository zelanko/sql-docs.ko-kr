---
title: 원본 및 대상 데이터베이스 매핑 (AccessToSQL) | Microsoft Docs
description: 여러 데이터베이스에 대 한 여러 데이터베이스를 포함 하 여 SQL Server 또는 Azure SQL Database에 대 한 액세스 데이터베이스 마이그레이션의 대상 데이터베이스를 지정 하는 방법을 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9e07c42e272728943f30198c8800c86aaa9443e3
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938163"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>원본 및 대상 데이터베이스 매핑 (AccessToSQL)
또는 SQL Azure에 연결 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 경우 마이그레이션할 대상 데이터베이스를 지정 해야 합니다. 여러 Access 데이터베이스를 사용 하는 경우 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 (또는 스키마) 또는 연결 된 Azure SQL Database 아래의 여러 스키마에 매핑할 수 있습니다.  
  
## <a name="sql-server-or-azure-sql-database-schemas"></a>스키마 SQL Server 또는 Azure SQL Database  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스는 스키마 개념을 사용 하 여 데이터베이스 내의 개체를 논리 그룹으로 구분 합니다. 예를 들어 라이브러리 데이터베이스는 **books**, **audio**및 **video** 라는 세 가지 스키마를 사용 하 여 책, 오디오 및 비디오 개체를 서로 구분할 수 있습니다. 기본적으로 access 데이터베이스는 SQL Azure의 **dbo** 연결 된 **master** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 **dbo** 스키마에 대 한 master 데이터베이스 및 dbo 스키마에 매핑됩니다.  
  
각 Access 데이터베이스와 데이터베이스 및 스키마 간의 매핑을 사용자 지정 하지 않는 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA는 access 데이터베이스와 연결 된 모든 스키마와 데이터를 매핑된 기본 데이터베이스로 마이그레이션합니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마 수정  
SSMA를 사용 하면 각 Access 데이터베이스를 또는 Azure SQL Database에 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 다음 절차에서는 데이터베이스당 매핑을 사용자 지정 하는 방법을 설명 합니다.  
  
**대상 데이터베이스 및 스키마를 수정 하려면**  
  
1.  액세스 메타 데이터 탐색기 창에서 **access-metadata**를 선택 합니다.  
  
    **데이터베이스** 노드 또는 데이터베이스 노드를 선택 하는 경우에도 스키마 매핑을 사용할 수 있습니다. 선택한 개체에 대해 스키마 매핑 목록이 사용자 지정 됩니다.  
  
2.  오른쪽 창에서 **스키마 매핑** 탭을 클릭 합니다.  
  
    Access 데이터베이스 이름과 해당 ssNoVersion 또는 Sql Azure 스키마를 포함 하는 테이블이 표시 됩니다. 대상 스키마는 두 부분으로 구성 된 표기법 (데이터베이스 스키마)로 표시 됩니다.  
  
3.  사용자 지정 하려는 매핑이 포함 된 행을 선택 하 고 **수정**을 클릭 합니다.  
  
4.  **대상 스키마 선택** 대화 상자에서 사용 가능한 대상 데이터베이스와 스키마를 찾아보거나 두 부분으로 구성 된 표기법 (데이터베이스 스키마)의 텍스트 상자에 데이터베이스 및 스키마 이름을 입력 한 다음 **확인을**클릭 합니다.  
  
**매핑 모드**  
  
-   SQL Server 매핑  
  
원본 데이터베이스를 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA를 사용 하 여 연결 된 대상 데이터베이스에 매핑됩니다. 매핑되는 대상 데이터베이스가에 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"데이터베이스 및/또는 스키마가 대상 메타 데이터에 없습니다." 라는 메시지가 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 동기화 중에 생성 됩니다. 계속 하 시겠습니까? "** 예를 클릭합니다. 마찬가지로, 동기화 중에 생성 되는 대상 데이터베이스의 기존이 아닌 스키마에 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   SQL Azure 매핑  
  
원본 데이터베이스를 연결 된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 또는 연결 된 대상 데이터베이스의 모든 스키마에 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 원본 스키마를 연결 된 대상 데이터베이스의 존재 하지 않는 스키마에 매핑하면 **"스키마가 대상 메타 데이터에 없습니다." 라는 메시지가 표시 됩니다. 동기화 중에 생성 됩니다. 계속 하 시겠습니까? "** 예를 클릭 합니다.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>초기 데이터베이스 및 스키마로 되돌리기  
Access 데이터베이스와 또는 Azure SQL Database 간의 매핑을 사용자 지정 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결 하거나 SQL Azure 때 지정한 데이터베이스로 다시 매핑을 되돌릴 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**기본 데이터베이스 및 스키마로 다시 설정 하려면**  
  
1.  스키마 매핑 탭에서 행을 선택 하 고 기본값으로 **다시 설정** 을 클릭 하 여 기본 데이터베이스 및 스키마로 되돌립니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [데이터베이스 개체를 변환](converting-access-database-objects-accesstosql.md) 하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  

---
title: 원본 및 대상 데이터베이스 (AccessToSQL) 매핑 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: acb6a8c71c3f144850cb9c24431bcff440cdf761
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392171"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>원본 및 대상 데이터베이스 (AccessToSQL) 매핑
에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 마이그레이션에 대 한 대상 데이터베이스를 지정 해야 합니다. Access 데이터베이스를 여러 개 있는 경우를 매핑할 수 있습니다 이러한 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 (또는 스키마) 또는 연결 된 SQL Azure 데이터베이스에서 여러 스키마입니다.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server 또는 SQL Azure 데이터베이스 스키마  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 데이터베이스 내의 개체를 논리 그룹으로 구분할 스키마의 개념을 사용 합니다. 라이브러리 데이터베이스 라는 세 개의 스키마를 사용할 수는 예를 들어 **책**를 **오디오**, 및 **비디오** 으로 책, 오디오 및 비디오 개체를 서로 분리 합니다. 기본적으로 access 데이터베이스에 매핑되 **마스터** 데이터베이스 및 **dbo** 스키마 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 연결 된 데이터베이스 및 **dbo** SQL Azure 대 한 스키마입니다.  
  
각 액세스 데이터베이스 간의 매핑을 사용자 지정 하지 않으면 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 스키마를 스키마 및 매핑된 기본 데이터베이스에 대 한 액세스 데이터베이스에 연결 된 데이터를 모든 SSMA 마이그레이션됩니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마를 수정합니다.  
SSMA는 각 액세스 데이터베이스에 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 및 스키마입니다. 다음 절차에는 데이터베이스당 매핑 사용자 지정 하는 방법을 설명 합니다.  
  
**대상 데이터베이스 및 스키마를 수정 하려면**  
  
1.  액세스 메타 데이터 탐색기 창에서 선택 **메타 데이터를 액세스할**합니다.  
  
    스키마 매핑 역시 사용할 수 있는 선택 된 **데이터베이스** 노드 또는 모든 데이터베이스 노드. 스키마 매핑 목록에 선택한 개체에 대 한 사용자 지정 됩니다.  
  
2.  오른쪽 창에서을 클릭 합니다 **스키마 매핑** 탭 합니다.  
  
    액세스를 포함 하는 테이블을 보면 데이터베이스 이름 및 해당 ssNoVersion 또는 Sql Azure 스키마입니다. 대상 스키마를 두 부분 (database.schema) 표기법으로 표시 됩니다.  
  
3.  사용자 지정 하 고 클릭 하려는 매핑을 포함 하는 행 선택 **수정**합니다.  
  
4.  에 **대상 스키마 선택** 대화 상자에서 사용할 수 있는 대상 데이터베이스 및 스키마 또는 데이터베이스와 스키마 2 부 표기법 (database.schema) 텍스트 상자에 이름과 클릭 형식에 대 한 찾아보기 있습니다 **확인**.  
  
**매핑 모드**  
  
-   SQL Server에 매핑  
  
원본 데이터베이스는 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스 매핑된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있는 연결한 SSMA를 사용 하 여 데이터베이스입니다. 매핑되는 대상 데이터베이스에 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 다음 메시지와 함께 나타납니다 **"데이터베이스 및/또는 스키마를 대상에 존재 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터입니다. 동기화 하는 동안 만들어집니다. 수행할 계속 하 시겠습니까 "?** 예를 클릭 합니다. 마찬가지로 존재 하지 않는 대상 스키마에 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동기화 하는 동안 만들어질 수 있는 데이터베이스입니다.  
  
-   SQL Azure 대 한 매핑  
  
원본 데이터베이스 연결 된 대상에 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 또는 모든 스키마에 연결 된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 연결 된 대상 데이터베이스에서 존재 하지 않는 스키마 원본 스키마를 매핑할 경우 묻는 메시지를 사용 하 여 **"스키마 대상 메타 데이터에는 존재 하지 않습니다. 동기화 하는 동안 만들어집니다. 계속 하 시겠습니까? "** 예를 클릭 합니다.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>초기 데이터베이스 및 스키마 되돌리기  
Access 데이터베이스 간의 매핑을 사용자 지정 하면와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 및 스키마에 연결 하는 경우 지정한 데이터베이스에 다시 매핑 되돌릴 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
**기본 데이터베이스 및 스키마를 다시 설정 하려면**  
  
1.  스키마 매핑 탭에서 모든 행을 선택 하 고 클릭 **기본값으로** 기본 데이터베이스 및 스키마를 되돌리려면 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  

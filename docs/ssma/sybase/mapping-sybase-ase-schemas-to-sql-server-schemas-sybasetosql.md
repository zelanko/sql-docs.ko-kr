---
title: Sybase ASE 스키마를 SQL Server 스키마 (SybaseToSQL)에 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2a27b2e7c915a1ac13050d0ed188002cd42746c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705934"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Sybase ASE 스키마를 SQL Server 스키마에 매핑(SybaseToSQL)
Sybase 적응형 Server Enterprise (ASE)에서 각 데이터베이스에 하나 이상의 스키마에 있습니다. 기본적으로 SSMA 동일한 데이터베이스와 스키마에서 데이터베이스 및 스키마 내의 모든 개체를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. ASE 간의 매핑을 사용자 지정할 수는 있지만 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터베이스 및 스키마입니다.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 및 SQL Server 또는 SQL Azure 스키마  
ASE와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 두 파트 표기법을 사용 하 여 데이터베이스와 해당 스키마를 지정 하는 SQL Azure 또는 *database.schema*합니다. ASE에서 예를 들어 **데모** 데이터베이스에 있을 수는 **dbo** 스키마입니다. 데이터베이스 및 스키마 쌍으로 지정 되어 있는지 **demo.dbo**합니다. 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 동일한 데이터베이스 및 스키마 쌍도로 지정 됩니다 **demo.dbo**합니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마를 수정합니다.  
SSMA에 매핑할 수 있습니다 ASE 스키마를 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 스키마입니다.  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  Sybase 메타 데이터 탐색기에서 선택 **데이터베이스**합니다.  
  
    **스키마 매핑** 탭 역시 사용할 수 있는 개별 데이터베이스를 선택 합니다 **스키마** 폴더 또는 개별 스키마입니다. 목록에는 **스키마 매핑** 탭은 선택한 개체에 대 한 사용자 지정 합니다.  
  
2.  오른쪽 창에서을 클릭 합니다 **스키마 매핑** 탭 합니다.  
  
    다음에 대상 값에 해당 스키마를 사용 하 여 모든 ASE 데이터베이스 목록이 표시 됩니다. 이 대상 표기법을 두 부분으로에서 표시 됩니다 (*database.schema*)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체와 데이터에 마이그레이션할 수 있습니다.  
  
3.  변경 하 고 클릭 하려는 매핑을 포함 하는 행 선택 **수정**합니다.  
  
4.  에 **대상 스키마 선택** 대화 상자에서 사용할 수 있는 대상 데이터베이스 및 스키마 또는 데이터베이스와 스키마 2 부 표기법 (database.schema) 텍스트 상자에 이름과 클릭 형식에 대 한 찾아보기 있습니다 **확인**.  
  
5.  대상에 변경 된 **스키마 매핑** 탭 합니다.  
  
**매핑 모드**  
  
-   SQL Server에 매핑  
  
원본 데이터베이스는 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스 매핑된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있는 연결한 SSMA를 사용 하 여 데이터베이스입니다. 매핑되는 대상 데이터베이스에 존재 하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 다음 메시지와 함께 나타납니다 **"데이터베이스 및/또는 스키마를 대상에 존재 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터입니다. 동기화 하는 동안 만들어집니다. 수행할 계속 하 시겠습니까 "?** 예를 클릭 합니다. 마찬가지로 존재 하지 않는 대상 스키마에 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동기화 하는 동안 만들어질 수 있는 데이터베이스입니다.  
  
-   SQL Azure 대 한 매핑  
  
연결 된 대상 SQL Azure 데이터베이스와 연결 된 대상 SQL Azure 데이터베이스의 모든 스키마에 원본 데이터베이스를 매핑할 수 있습니다. 연결 된 대상 데이터베이스에서 존재 하지 않는 스키마 원본 스키마를 매핑할 경우 묻는 메시지를 사용 하 여 **"스키마 대상 메타 데이터에는 존재 하지 않습니다. 동기화 하는 동안 만들어집니다. 계속 하 시겠습니까? "** 예를 클릭 합니다.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마를 되돌리기  
ASE 스키마 간의 매핑을 사용자 지정 하면 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 스키마 매핑을 다시 기본 값으로 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마를 되돌리려면**  
  
1.  스키마 매핑 탭에서 모든 행을 선택 하 고 클릭 **기본값으로** 기본 데이터베이스 및 스키마를 되돌리려면 합니다.  
  
## <a name="next-steps"></a>다음 단계  
Sybase ASE 개체를 변환 하는 분석 하려는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체를 할 수 있습니다 [변환 보고서를 만드는](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)합니다. 수이 고, 그렇지 [ASE 데이터베이스 개체 정의 변환](converting-sybase-ase-database-objects-sybasetosql.md) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체를 정의 합니다.  
  
## <a name="see-also"></a>관련 항목  
[Sybase ASE 데이터베이스를 SQL Server-Azure SQL DB로 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

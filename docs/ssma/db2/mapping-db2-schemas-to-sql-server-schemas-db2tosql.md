---
title: "DB2 스키마를 SQL Server 스키마 (DB2ToSQL)로 매핑 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19abc8a901b2241a4fa7d6c69da2ffd90b77afb9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>DB2 스키마를 SQL Server 스키마 (DB2ToSQL)로 매핑
D b 2에서는 각 데이터베이스에는 하나 이상의 스키마에 있습니다. 기본적으로 SSMA를 DB2 스키마의 모든 개체를 마이그레이션합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마에 대 한 명명 된 데이터베이스입니다. 그러나 DB2 스키마 간의 매핑을 사용자 지정할 수는 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스.  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 및 SQL Server 스키마  
DB2 데이터베이스 스키마가 포함 되어 있습니다. 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마 여러 개 있을 수 있으며 각 여러 개의 데이터베이스를 포함 합니다.  
  
스키마의 DB2 개념에 매핑됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개념 데이터베이스 및 해당 스키마 중 하나입니다. 예를 들어 d b 2 라는 스키마 해야할 **HR**합니다. 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 라는 데이터베이스가 있을 수 **HR**, 해당 데이터베이스 내에서 스키마는 및입니다. 하나의 스키마가는 **dbo** (또는 데이터베이스 소유자) 스키마. 기본적으로 DB2 스키마 **HR** 에 매핑할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 및 스키마 **HR.dbo**합니다. SSMA 참조 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마로 데이터베이스와 스키마의 조합입니다.  
  
DB2 간의 매핑을 수정할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마입니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마를 수정합니다.  
SSMA를 매핑할 수는 DB2 스키마에 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마입니다.  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  DB2 메타 데이터 탐색기에서 선택 **스키마**합니다.  
  
    **스키마 매핑** 개별 데이터베이스를 선택 하면 탭은 또한 사용할 수는 **스키마** 폴더 또는 개별 스키마입니다. 목록에는 **스키마 매핑** 탭은 선택한 개체에 대 한 사용자 지정 합니다.  
  
2.  오른쪽 창에서 클릭 하 고 **스키마 매핑** 탭 합니다.  
  
    다음 대상 값 모든 DB2 스키마의 목록이 표시 됩니다. 이 대상은 두 부분으로 구성 표기법으로 표시 됩니다 (*database.schema*)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체와 데이터 마이그레이션할 수 있습니다.  
  
3.  클릭 하 고, 변경 하려는 매핑을 포함 하는 행 선택 **수정**합니다.  
  
    에 **대상 스키마 선택** 대화 상자에서 검색할 수 있습니다. 사용 가능한 대상 데이터베이스 및 스키마 또는 두 부분으로 구성 표기법 (database.schema)의 텍스트 상자에 이름을 지정 하 고 클릭 한 다음 데이터베이스 및 스키마 형식에 대 한 **확인**합니다.  
  
4.  대상 변경 되는 **스키마 매핑** 탭 합니다.  
  
**매핑 모드**  
  
-   SQL Server에 매핑  
  
원본 데이터베이스는 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스 매핑된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA를 사용 하 여 연결가 있는 데이터베이스입니다. 매핑되는 대상 데이터베이스에 존재 하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 묻는 메시지를 사용 하는 다음 **"데이터베이스 및/또는 스키마 대상에 존재 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터입니다. 해당 하는 동기화 하는 동안 만들어졌습니다. 마십시오 계속 하 시겠습니까 "?** 예를 클릭 합니다. 마찬가지로, 대상에서 존재 하지 않는 스키마를 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 동기화 중에 생성 되는 데이터베이스입니다.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마에 되돌리기  
DB2 스키마 간의 매핑을 사용자 지정 하는 경우와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마를 기본 값으로 다시 매핑 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마로 되돌리려면**  
  
1.  스키마 매핑 탭에서 모든 행을 선택 하 고 클릭 **기본값으로 재설정** 기본 데이터베이스 및 스키마에 되돌릴 수 있습니다.  
  
## <a name="next-steps"></a>Next Steps  
DB2 개체를 변환 하는 과정을 분석 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체를 할 수 있습니다 [데이터 마이그레이션 보고서 (SSMA 공통)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server &#40; DB2eToSQL &#41;에 연결](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[SQL Server &#40; DB2ToSQL &#41; DB2 데이터베이스 마이그레이션](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

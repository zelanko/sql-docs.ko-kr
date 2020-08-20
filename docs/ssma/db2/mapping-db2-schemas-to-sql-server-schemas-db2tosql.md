---
description: SQL Server 스키마에 DB2 스키마 매핑 (DB2ToSQL)
title: SQL Server 스키마에 DB2 스키마 매핑 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a5c60984f9f1ed8da7238c254ac8b939dc1a9dee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472513"
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>SQL Server 스키마에 DB2 스키마 매핑 (DB2ToSQL)
DB2에서 각 데이터베이스에는 하나 이상의 스키마가 있습니다. 기본적으로 SSMA는 DB2 스키마의 모든 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마에 대해 라는 데이터베이스로 마이그레이션합니다. 그러나 DB2 스키마와 데이터베이스 간의 매핑을 사용자 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 및 SQL Server 스키마  
DB2 데이터베이스에는 스키마가 포함 되어 있습니다. 인스턴스는 여러 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 포함 하며 각 데이터베이스에는 여러 스키마가 있을 수 있습니다.  
  
스키마의 DB2 개념은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 개념과 스키마 중 하나에 매핑됩니다. 예를 들어 DB2에는 **HR**이라는 이름의 스키마가 있을 수 있습니다. 인스턴스에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **HR**이라는 데이터베이스가 있고 해당 데이터베이스 내에는 스키마가 있을 수 있습니다. 한 스키마는 **dbo** (또는 데이터베이스 소유자) 스키마입니다. 기본적으로 DB2 스키마 **hr** 은 데이터베이스 및 스키마에 매핑됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **dbo**. SSMA는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 스키마의 조합을 스키마로 나타냅니다.  
  
DB2와 스키마 간의 매핑을 수정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마 수정  
SSMA에서 DB2 스키마를 사용 가능한 스키마에 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  DB2 메타 데이터 탐색기에서 **스키마**를 선택 합니다.  
  
    **스키마 매핑** 탭은 개별 데이터베이스, **스키마** 폴더 또는 개별 스키마를 선택 하는 경우에도 사용할 수 있습니다. **스키마 매핑** 탭의 목록은 선택한 개체에 대해 사용자 지정 됩니다.  
  
2.  오른쪽 창에서 **스키마 매핑** 탭을 클릭 합니다.  
  
    모든 DB2 스키마 목록에 대상 값이 표시 됩니다. 이 대상은 개체와 데이터가 마이그레이션되는 두 부분으로 구성 된 표기법 (*데이터베이스 스키마*)에서 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  변경 하려는 매핑이 포함 된 행을 선택 하 고 **수정**을 클릭 합니다.  
  
    **대상 스키마 선택** 대화 상자에서 사용 가능한 대상 데이터베이스와 스키마를 찾아보거나 두 부분으로 구성 된 표기법 (데이터베이스 스키마)의 텍스트 상자에 데이터베이스 및 스키마 이름을 입력 한 다음 **확인을**클릭 합니다.  
  
4.  대상은 **스키마 매핑** 탭에서 변경 됩니다.  
  
**매핑 모드**  
  
-   SQL Server 매핑  
  
원본 데이터베이스를 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA를 사용 하 여 연결 된 대상 데이터베이스에 매핑됩니다. 매핑되는 대상 데이터베이스가 존재 하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"데이터베이스 및/또는 스키마가 대상 메타 데이터에 없습니다." 라는 메시지가 표시 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 동기화 중에 생성 됩니다. 계속 하 시겠습니까? "** 예를 클릭합니다. 마찬가지로, 동기화 중에 생성 되는 대상 데이터베이스의 기존이 아닌 스키마에 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마로 되돌리기  
DB2 스키마와 스키마 간의 매핑을 사용자 지정 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 매핑을 다시 기본값으로 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마로 되돌리려면**  
  
1.  스키마 매핑 탭에서 행을 선택 하 고 기본값으로 **다시 설정** 을 클릭 하 여 기본 데이터베이스 및 스키마로 되돌립니다.  
  
## <a name="next-steps"></a>다음 단계  
DB2 개체를 개체로 변환 하는 과정을 분석 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ssma (데이터 마이그레이션 보고서)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)를 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server &#40;DB2eToSQL&#41;에 연결 하는 중 ](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[DB2 데이터베이스를 SQL Server &#40;DB2ToSQL&#41;로 마이그레이션 ](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

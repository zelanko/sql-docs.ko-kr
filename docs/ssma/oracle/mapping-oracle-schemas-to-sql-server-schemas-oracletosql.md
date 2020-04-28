---
title: Oracle 스키마를 SQL Server 스키마에 매핑 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e375c07ceddc995b599930c14f00710af040d6c0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68262908"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Oracle 스키마를 SQL Server 스키마에 매핑(OracleToSQL)
Oracle에서 각 데이터베이스에는 하나 이상의 스키마가 있습니다. 기본적으로 SSMA는 Oracle 스키마의 모든 개체를 스키마에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 라는 데이터베이스로 마이그레이션합니다. 그러나 Oracle 스키마와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 간의 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle 및 SQL Server 스키마  
Oracle 데이터베이스는 스키마를 포함 합니다. 인스턴스는 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개의 데이터베이스를 포함 하며 각 데이터베이스에는 여러 스키마가 있을 수 있습니다.  
  
스키마의 Oracle 개념은 데이터베이스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개념과 스키마 중 하나에 매핑됩니다. 예를 들어 Oracle에는 **HR**이라는 스키마가 있을 수 있습니다. 인스턴스에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **HR**이라는 데이터베이스가 있고 해당 데이터베이스 내에는 스키마가 있을 수 있습니다. 한 스키마는 **dbo** (또는 데이터베이스 소유자) 스키마입니다. 기본적으로 Oracle 스키마 **hr** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 스키마에 매핑됩니다. **dbo**. SSMA는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 스키마의 조합을 스키마로 나타냅니다.  
  
Oracle과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마 간의 매핑을 수정할 수 있습니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마 수정  
SSMA에서 Oracle 스키마를 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마에 매핑할 수 있습니다.  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  Oracle 메타 데이터 탐색기에서 **스키마**를 선택 합니다.  
  
    **스키마 매핑** 탭은 개별 데이터베이스, **스키마** 폴더 또는 개별 스키마를 선택 하는 경우에도 사용할 수 있습니다. **스키마 매핑** 탭의 목록은 선택한 개체에 대해 사용자 지정 됩니다.  
  
2.  오른쪽 창에서 **스키마 매핑** 탭을 클릭 합니다.  
  
    모든 Oracle 스키마 목록에 대상 값이 표시 됩니다. 이 대상은 개체와 데이터가 마이그레이션되는 두 부분으로 구성 된 표기법 (*데이터베이스 스키마*) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 표시 됩니다.  
  
3.  변경 하려는 매핑이 포함 된 행을 선택 하 고 **수정**을 클릭 합니다.  
  
    **대상 스키마 선택** 대화 상자에서 사용 가능한 대상 데이터베이스와 스키마를 찾아보거나 두 부분으로 구성 된 표기법 (데이터베이스 스키마)의 텍스트 상자에 데이터베이스 및 스키마 이름을 입력 한 다음 **확인을**클릭 합니다.  
  
4.  대상은 **스키마 매핑** 탭에서 변경 됩니다.  
  
**매핑 모드**  
  
-   SQL Server 매핑  
  
원본 데이터베이스를 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스는 SSMA를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 연결 된 대상 데이터베이스에 매핑됩니다. 매핑되는 대상 데이터베이스가 존재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하지 않는 경우 **"데이터베이스 및/또는 스키마가 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터에 없습니다." 라는 메시지가 표시 됩니다. 동기화 중에 생성 됩니다. 계속 하 시겠습니까? "** 예를 클릭합니다. 마찬가지로, 동기화 중에 생성 되는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 기존이 아닌 스키마에 스키마를 매핑할 수 있습니다.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마로 되돌리기  
Oracle 스키마와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마 간의 매핑을 사용자 지정 하는 경우 매핑을 다시 기본값으로 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마로 되돌리려면**  
  
1.  스키마 매핑 탭에서 행을 선택 하 고 기본값으로 **다시 설정** 을 클릭 하 여 기본 데이터베이스 및 스키마로 되돌립니다.  
  
## <a name="next-steps"></a>다음 단계  
Oracle 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체로 변환 하는 과정을 분석 하려는 경우에는 [변환 보고서를 만들](assessing-oracle-schemas-for-conversion-oracletosql.md)수 있습니다. 그렇지 않으면 [Oracle 데이터베이스 개체 정의를](converting-oracle-schemas-oracletosql.md) 개체 정의로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server &#40;OracleToSQL&#41;에 연결 하는 중](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

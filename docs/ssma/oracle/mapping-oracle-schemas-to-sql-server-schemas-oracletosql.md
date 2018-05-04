---
title: Oracle 스키마를 SQL Server 스키마 (OracleToSQL)로 매핑 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 91aa5097f4117c12a6d53af83f6a5e6a6ee68cd2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Oracle 스키마를 SQL Server 스키마 (OracleToSQL)로 매핑
Oracle의 경우 각 데이터베이스에는 하나 이상의 스키마에 있습니다. 기본적으로 SSMA를 Oracle 스키마의 모든 개체를 마이그레이션합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마에 대 한 명명 된 데이터베이스입니다. 그러나 Oracle 스키마 간의 매핑을 사용자 지정할 수는 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스.  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle 및 SQL Server 스키마  
Oracle 데이터베이스 스키마가 포함 되어 있습니다. 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마 여러 개 있을 수 있으며 각 여러 개의 데이터베이스를 포함 합니다.  
  
스키마의 Oracle 개념에 매핑됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개념 데이터베이스 및 해당 스키마 중 하나입니다. 예를 들어 Oracle 라는 스키마 해야할 **HR**합니다. 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 라는 데이터베이스가 있을 수 **HR**, 해당 데이터베이스 내에서 스키마는 및입니다. 하나의 스키마가는 **dbo** (또는 데이터베이스 소유자) 스키마. 기본적으로 Oracle 스키마 **HR** 에 매핑할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 및 스키마 **HR.dbo**합니다. SSMA 참조 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마로 데이터베이스와 스키마의 조합입니다.  
  
Oracle 간의 매핑을 수정할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마입니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마를 수정합니다.  
SSMA를 매핑할 수는 Oracle 스키마에 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마입니다.  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  Oracle 메타 데이터 탐색기에서 선택 **스키마**합니다.  
  
    **스키마 매핑** 개별 데이터베이스를 선택 하면 탭은 또한 사용할 수는 **스키마** 폴더 또는 개별 스키마입니다. 목록에는 **스키마 매핑** 탭은 선택한 개체에 대 한 사용자 지정 합니다.  
  
2.  오른쪽 창에서 클릭 하 고 **스키마 매핑** 탭 합니다.  
  
    다음 대상 값 모든 Oracle 스키마의 목록이 표시 됩니다. 이 대상은 두 부분으로 구성 표기법으로 표시 됩니다 (*database.schema*)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체와 데이터 마이그레이션할 수 있습니다.  
  
3.  클릭 하 고, 변경 하려는 매핑을 포함 하는 행 선택 **수정**합니다.  
  
    에 **대상 스키마 선택** 대화 상자에서 검색할 수 있습니다. 사용 가능한 대상 데이터베이스 및 스키마 또는 두 부분으로 구성 표기법 (database.schema)의 텍스트 상자에 이름을 지정 하 고 클릭 한 다음 데이터베이스 및 스키마 형식에 대 한 **확인**합니다.  
  
4.  대상 변경 되는 **스키마 매핑** 탭 합니다.  
  
**매핑 모드**  
  
-   SQL Server에 매핑  
  
원본 데이터베이스는 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스 매핑된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA를 사용 하 여 연결가 있는 데이터베이스입니다. 매핑되는 대상 데이터베이스에 존재 하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 묻는 메시지를 사용 하는 다음 **"데이터베이스 및/또는 스키마 대상에 존재 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터입니다. 해당 하는 동기화 하는 동안 만들어졌습니다. 마십시오 계속 하 시겠습니까 "?** 예를 클릭 합니다. 마찬가지로, 대상에서 존재 하지 않는 스키마를 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 동기화 중에 생성 되는 데이터베이스입니다.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마에 되돌리기  
Oracle 스키마 간의 매핑을 사용자 지정 하는 경우와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 스키마를 기본 값으로 다시 매핑 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마로 되돌리려면**  
  
1.  스키마 매핑 탭에서 모든 행을 선택 하 고 클릭 **기본값으로 재설정** 기본 데이터베이스 및 스키마에 되돌릴 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계  
Oracle 개체를 변환 하는 과정을 분석 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체를 할 수 있습니다 [변환 보고서를 만들](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357)합니다. 수 그렇지 않으면 [Oracle 데이터베이스 개체 정의 변환](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체 정의 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 연결 &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[SQL Server로 데이터베이스 마이그레이션 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

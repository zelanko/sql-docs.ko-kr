---
title: Sybase ASE 스키마를 SQL Server 스키마 (SybaseToSQL)로 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1e0b8dad8d5742782ed3b3828806c5122092b37b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Sybase ASE 스키마를 SQL Server 스키마 (SybaseToSQL)로 매핑
Sybase 적응형 Server Enterprise (ASE), 각 데이터베이스에 하나 이상의 스키마에 있습니다. 기본적으로 SSMA는 동일한 데이터베이스 및 스키마에 데이터베이스 및 스키마 내의 모든 개체를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 그러나 ASE 간의 매핑을 사용자 지정할 수는 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 데이터베이스 및 스키마입니다.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 및 SQL Server 또는 SQL Azure 스키마  
ASE 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 으로 두 개의 부분 표기법을 사용 하 여 데이터베이스와 해당 스키마를 지정 하는 SQL Azure 또는 *database.schema*합니다. 예를 들어 ASE에에서 **데모** 있을 수 있습니다, 데이터베이스는 **dbo** 스키마입니다. 데이터베이스 및 스키마 쌍으로 지정 된 **demo.dbo**합니다. 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 아니면 SQL Azure는 동일한 데이터베이스 및 스키마를 쌍도로 지정 **demo.dbo**합니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마를 수정합니다.  
SSMA를 매핑할 수 ASE 스키마에 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 스키마입니다.  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  Sybase 메타 데이터 탐색기에서 선택 **데이터베이스**합니다.  
  
    **스키마 매핑** 개별 데이터베이스를 선택 하면 탭은 또한 사용할 수는 **스키마** 폴더 또는 개별 스키마입니다. 목록에는 **스키마 매핑** 탭은 선택한 개체에 대 한 사용자 지정 합니다.  
  
2.  오른쪽 창에서 클릭 하 고 **스키마 매핑** 탭 합니다.  
  
    다음 대상 값의 스키마와 함께 모든 ASE 데이터베이스 목록이 표시 됩니다. 이 대상은 두 부분으로 구성 표기법으로 표시 됩니다 (*database.schema*)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체와 데이터 마이그레이션할 수 있습니다.  
  
3.  클릭 하 고, 변경 하려는 매핑을 포함 하는 행 선택 **수정**합니다.  
  
4.  에 **대상 스키마 선택** 대화 상자에서 검색할 수 있습니다. 사용 가능한 대상 데이터베이스 및 스키마 또는 두 부분으로 구성 표기법 (database.schema)의 텍스트 상자에 이름을 지정 하 고 클릭 한 다음 데이터베이스 및 스키마 형식에 대 한 **확인**합니다.  
  
5.  대상 변경 되는 **스키마 매핑** 탭 합니다.  
  
**매핑 모드**  
  
-   SQL Server에 매핑  
  
원본 데이터베이스는 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스 매핑된 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA를 사용 하 여 연결가 있는 데이터베이스입니다. 매핑되는 대상 데이터베이스에 존재 하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 묻는 메시지를 사용 하는 다음 **"데이터베이스 및/또는 스키마 대상에 존재 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터입니다. 해당 하는 동기화 하는 동안 만들어졌습니다. 마십시오 계속 하 시겠습니까 "?** 예를 클릭 합니다. 마찬가지로, 대상에서 존재 하지 않는 스키마를 스키마를 매핑할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 동기화 중에 생성 되는 데이터베이스입니다.  
  
-   SQL Azure에 매핑  
  
원본 데이터베이스를 연결 된 대상 SQL Azure 데이터베이스 또는 연결 된 대상 SQL Azure 데이터베이스의 모든 스키마에 매핑할 수 있습니다. 연결 된 대상 데이터베이스에서 어떤 존재 하지 않는 스키마 소스 스키마를 매핑할 경우 다음 메시지와 함께 나타납니다 **"스키마 대상 메타 데이터에는 존재 하지 않습니다. 해당 하는 동기화 하는 동안 만들어졌습니다. 계속 하 시겠습니까? "** 예를 클릭 합니다.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마에 되돌리기  
ASE 스키마 간의 매핑을 사용자 지정 하는 경우와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 스키마를 기본 값으로 다시 매핑 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마로 되돌리려면**  
  
1.  스키마 매핑 탭에서 모든 행을 선택 하 고 클릭 **기본값으로 재설정** 기본 데이터베이스 및 스키마에 되돌릴 수 있습니다.  
  
## <a name="next-steps"></a>Next Steps  
Sybase ASE 개체를 변환 하는 과정을 분석 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체를 할 수 있습니다 [변환 보고서를 만들](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)합니다. 수 그렇지 않으면 [ASE 데이터베이스 개체 정의 변환](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체를 정의 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[Azure SQL DB &#40; SQL Server-Sybase ASE 데이터베이스 마이그레이션 SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

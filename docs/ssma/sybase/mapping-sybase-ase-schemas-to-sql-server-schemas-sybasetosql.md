---
title: SQL Server 스키마에 Sybase ASE 스키마 매핑 (SybaseToSQL) | Microsoft Docs
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
ms.openlocfilehash: 5c39e81f8faffed606e6ca94315c47d383174c91
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028873"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Sybase ASE 스키마를 SQL Server 스키마에 매핑(SybaseToSQL)
Sybase 적응 서버 엔터프라이즈 (ASE)에서 각 데이터베이스에는 하나 이상의 스키마가 있습니다. 기본적으로 SSMA는 데이터베이스 및 스키마 내의 모든 개체를 또는 SQL Azure의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동일한 데이터베이스 및 스키마로 마이그레이션합니다. 그러나 ASE와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 데이터베이스 및 스키마 간의 매핑을 사용자 지정할 수 있습니다.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 및 SQL Server 또는 SQL Azure 스키마  
ASE 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or SQL Azure는 두 부분으로 구성 된 표기법을 사용 하 여 데이터베이스와 해당 스키마를 지정 합니다. *스키마*. 예를 들어 ASE **데모** 데이터베이스에 **dbo** 스키마가 있을 수 있습니다. 해당 데이터베이스 및 스키마 쌍은 **demo**로 지정 됩니다. 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure에 동일한 데이터베이스와 스키마가 있는 경우에는이 쌍도 **demo**로 지정 됩니다.  
  
## <a name="modifying-the-target-database-and-schema"></a>대상 데이터베이스 및 스키마 수정  
SSMA에서 ASE 스키마를 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스키마 또는 SQL Azure 스키마에 매핑할 수 있습니다.  
  
**데이터베이스 및 스키마를 수정 하려면**  
  
1.  Sybase 메타 데이터 탐색기에서 **데이터베이스**를 선택 합니다.  
  
    **스키마 매핑** 탭은 개별 데이터베이스, **스키마** 폴더 또는 개별 스키마를 선택 하는 경우에도 사용할 수 있습니다. **스키마 매핑** 탭의 목록은 선택한 개체에 대해 사용자 지정 됩니다.  
  
2.  오른쪽 창에서 **스키마 매핑** 탭을 클릭 합니다.  
  
    스키마가 있는 모든 ASE 데이터베이스 목록과 대상 값이 차례로 표시 됩니다. 이 대상은에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 두 부분으로 구성 된 표기법 (*데이터베이스 스키마*) 또는 개체와 데이터가 마이그레이션되는 SQL Azure 표시 됩니다.  
  
3.  변경 하려는 매핑이 포함 된 행을 선택 하 고 **수정**을 클릭 합니다.  
  
4.  **대상 스키마 선택** 대화 상자에서 사용 가능한 대상 데이터베이스와 스키마를 찾아보거나 두 부분으로 구성 된 표기법 (데이터베이스 스키마)의 텍스트 상자에 데이터베이스 및 스키마 이름을 입력 한 다음 **확인을**클릭 합니다.  
  
5.  대상은 **스키마 매핑** 탭에서 변경 됩니다.  
  
**매핑 모드**  
  
-   SQL Server 매핑  
  
원본 데이터베이스를 대상 데이터베이스에 매핑할 수 있습니다. 기본적으로 원본 데이터베이스는 SSMA를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 연결 된 대상 데이터베이스에 매핑됩니다. 매핑되는 대상 데이터베이스가 존재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]하지 않는 경우 **"데이터베이스 및/또는 스키마가 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메타 데이터에 없습니다." 라는 메시지가 표시 됩니다. 동기화 중에 생성 됩니다. 계속 하 시겠습니까? "** 예를 클릭합니다. 마찬가지로, 동기화 중에 생성 되는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 기존이 아닌 스키마에 스키마를 매핑할 수 있습니다.  
  
-   SQL Azure 매핑  
  
원본 데이터베이스를 연결 된 대상 SQL Azure 데이터베이스 또는 연결 된 대상 SQL Azure 데이터베이스의 모든 스키마에 매핑할 수 있습니다. 원본 스키마를 연결 된 대상 데이터베이스의 존재 하지 않는 스키마에 매핑하면 **"스키마가 대상 메타 데이터에 없습니다." 라는 메시지가 표시 됩니다. 동기화 중에 생성 됩니다. 계속 하 시겠습니까? "** 예를 클릭 합니다.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>기본 데이터베이스 및 스키마로 되돌리기  
ASE 스키마와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 스키마 간의 매핑을 사용자 지정 하는 경우 매핑을 다시 기본값으로 되돌릴 수 있습니다.  
  
**기본 데이터베이스 및 스키마로 되돌리려면**  
  
1.  스키마 매핑 탭에서 행을 선택 하 고 기본값으로 **다시 설정** 을 클릭 하 여 기본 데이터베이스 및 스키마로 되돌립니다.  
  
## <a name="next-steps"></a>다음 단계  
Sybase ASE 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체로 변환 하는 과정을 분석 하려면 [변환 보고서를 만들](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)수 있습니다. 그렇지 않으면 [ASE 데이터베이스 개체 정의를](converting-sybase-ase-database-objects-sybasetosql.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체 정의로 변환할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[Sybase ASE 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

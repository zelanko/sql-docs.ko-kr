---
title: SQL Server로 Access 데이터 마이그레이션-Azure SQL DB (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8f0e93efee0c57c904c32ec52fbb560f973f21b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907140"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>SQL Server로 Access 데이터 마이그레이션-Azure SQL DB (AccessToSQL)
로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스 개체를 성공적으로 만든 후에는에 대 한 액세스에서 또는 SQL Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 으로 데이터를 마이그레이션할 수 있습니다.  
  
## <a name="setting-migration-options"></a>마이그레이션 옵션 설정  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터를 마이그레이션하기 전에 **프로젝트 설정** 대화 상자에서 프로젝트 마이그레이션 옵션을 검토 하십시오. 이 대화 상자에서 마이그레이션 일괄 처리 크기, 테이블 잠금, 제약 조건 확인, 삽입 트리거 발생, id 및 null 값 처리 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 범위를 벗어난 날짜를 처리 하는 방법을 설정할 수 있습니다. 자세한 내용은 [프로젝트 설정 (마이그레이션)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)을 참조 하세요.  
  
## <a name="migrating-data"></a>데이터 마이그레이션  
데이터 마이그레이션은 트랜잭션 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 데이터 행을 이동 하는 대량 로드 작업입니다. 각 트랜잭션에서 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 되거나 SQL Azure 되는 행 수는 프로젝트 설정에서 구성 됩니다.  
  
마이그레이션 메시지를 보려면 출력 창이 표시 되는지 확인 합니다. 표시 되지 않는 경우 **보기** 메뉴에서 **출력**을 선택 합니다.  
  
**데이터를 마이그레이션하려면**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 액세스 데이터베이스 개체를 로드 했는지 확인 합니다.  
  
2.  액세스 메타 데이터 탐색기에서 마이그레이션할 데이터가 포함 된 개체를 선택 합니다.  
  
    -   전체 데이터베이스에 대 한 데이터를 마이그레이션하려면 데이터베이스 이름 옆의 확인란을 선택 합니다.  
  
    -   개별 테이블에서 데이터를 마이그레이션하려면 데이터베이스를 확장 하 고 **테이블**을 확장 한 다음 테이블 옆의 확인란을 선택 합니다. 개별 테이블에서 데이터를 생략 하려면 확인란의 선택을 취소 합니다.  
  
3.  **데이터베이스** 를 마우스 오른쪽 단추로 클릭 한 다음 **데이터 마이그레이션**을 선택 합니다.  
  
또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp** 명령줄 유틸리티 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 사용 하 여 ssma 외부에서 데이터를 마이그레이션할 수 있습니다. 이러한 도구에 대 한 자세한 내용은 온라인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설명서를 참조 하십시오.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 후에도 계속 사용 하려는 데이터베이스 응용 프로그램에 액세스 하는 경우 Access 데이터베이스 테이블을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블에 연결 합니다. 자세한 내용은 [SQL Server에 액세스 응용 프로그램 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[변환 및 마이그레이션 옵션 설정](setting-conversion-and-migration-options-accesstosql.md)  
  

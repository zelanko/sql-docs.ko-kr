---
title: 액세스 데이터를 Azure SQL DB (AccessToSQL)-SQL Server로 마이그레이션 | Microsoft Docs
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
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 38301e26dbe4b39a2be873a2154ec791c3c9a3f6
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773879"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>액세스 데이터를 Azure SQL DB (AccessToSQL)-SQL Server로 마이그레이션
가 데이터베이스 개체를 성공적으로 만든 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에 대 한 액세스에서 데이터를 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
## <a name="setting-migration-options"></a>마이그레이션 옵션 설정  
데이터를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure에 프로젝트 마이그레이션 옵션을 검토 하 고 **프로젝트 설정** 대화 상자. 이 대화 상자에서 마이그레이션 일괄 처리 크기, 테이블 잠금, 제약 조건 검사를 삽입 트리거 실행, id 및 처리, null 값 및 날짜 중에 처리 하는 방법을 설정할 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 범위입니다. 자세한 내용은 참조 [프로젝트 설정 (마이그레이션)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)합니다.  
  
## <a name="migrating-data"></a>데이터 마이그레이션  
마이그레이션 데이터는 행의 데이터를 이동 하는 대량 로드 작업 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 트랜잭션에서 합니다. 에 로드 하는 행 수가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 각 트랜잭션에서 SQL Azure 프로젝트 설정에서 구성 합니다.  
  
마이그레이션 메시지를 보려면 출력 창이 표시 되는지 확인 합니다. 그렇지 않을 경우에 **보기** 메뉴 선택 **출력**합니다.  
  
**데이터를 마이그레이션**  
  
1.  Access 데이터베이스 개체에 로드 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
2.  액세스 메타 데이터 탐색기에서 마이그레이션할 데이터가 포함 된 개체를 선택 합니다.  
  
    -   전체 데이터베이스에 대 한 데이터를 마이그레이션하려면 데이터베이스 이름 옆에 있는 확인란을 선택 합니다.  
  
    -   개별 테이블에서 데이터를 마이그레이션하려면 데이터베이스를 확장 하 고 **테이블**, 한 다음 테이블 옆의 확인란을 선택 합니다. 개별 테이블의에서 데이터를 생략 하려면 확인란의 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **데이터베이스** 선택한 후 **데이터 마이그레이션**합니다.  
  
또한를 사용 하 여 SSMA 외부에서 데이터를 마이그레이션할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bcp** 명령줄 유틸리티 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]합니다. 이러한 도구에 대 한 자세한 내용은 참조 하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 후 사용을 계속 하려면는 Access 데이터베이스 응용 프로그램, 있는 경우 연결을 Access 데이터베이스 테이블에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 테이블입니다. 자세한 내용은 참조 [SQL Server에 액세스 응용 프로그램 연결](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[설정 변환 및 마이그레이션 옵션](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)  
  

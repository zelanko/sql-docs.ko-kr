---
title: Access 데이터베이스 (AccessToSQL) 마이그레이션에 대 한 준비 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 9495ff7a58da124255cc6bf5674d92ebeef4c2b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299475"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Access 데이터베이스 (AccessToSQL) 마이그레이션 준비
Access 데이터베이스를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 마이그레이션하고 해당 데이터베이스 마이그레이션에 대 한 준비 되었는지 확인 하는 데이터베이스를 결정 해야 합니다.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>SQL Server로 마이그레이션할 시기 결정  
Jet 데이터베이스 엔진에 사용 되는 데이터베이스 엔진 액세스에 대 한 데이터 관리를 위한 유연 하 고 사용 하기 쉬운 솔루션을입니다. 그러나 커질수록 데이터베이스와 더 많은 업무에 중요 한 많은 사용자가 찾을 이들이 필요로 하는 뛰어난 성능, 보안 또는 가용성. 보다 강력한 데이터 플랫폼을 필요로 하는 응용 프로그램의 경우 해당 응용 프로그램에 대 한 기본 데이터베이스를 이동할 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 마이그레이션 시기를 결정 하는 방법에 대 한 자세한 내용은 참조는 [마이그레이션 정보 페이지](https://go.microsoft.com/fwlink/?LinkId=68571) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 웹 사이트입니다.  
  
데이터베이스를 마이그레이션한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결 된 테이블을 사용 하 여 액세스를 사용 하는 것, 응용 프로그램을 수동으로 마이그레이션할 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 직접 상호 작용 하는.NET Framework 기반 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="determining-which-databases-to-migrate"></a>마이그레이션할 데이터베이스를 결정 합니다.  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) 액세스를 Access 데이터베이스를 찾을 수 있습니다. 그런 다음 해당 데이터베이스에 대 한 메타 데이터를 내보낼 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 내보내기 및 메타 데이터를 쿼리 하는 방법에 대 한 자세한 내용은 참조 하세요. [Access 인벤토리 내보내기](exporting-an-access-inventory-accesstosql.md)합니다.  

   > [!NOTE]
   > 일부 기능에 액세스 및 설정, 지 또는으로 쉽게 변환 될 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 마이그레이션하기 전에 데이터베이스를 참조 하세요 [호환 되지 않는 기능에 액세스](incompatible-access-features-accesstosql.md)합니다.
  
## <a name="preparing-for-migration"></a>마이그레이션 준비  
다음 지침을 사용 하 여 Access 데이터베이스에 마이그레이션을 준비 하는 데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
### <a name="upgrading-older-access-databases"></a>이전의 Access 데이터베이스를 업그레이드합니다.  
Access 용 SSMA는 Access 97 및 이상 버전을 지원합니다. 이전 버전의 Access에서 데이터베이스에 있는 경우 열고 Access 97 이상에서 데이터베이스를 저장 합니다.  
  
### <a name="removing-workgroup-protection"></a>작업 그룹 보호를 제거합니다.  
SSMA는 작업 그룹 보호를 사용 하는 데이터베이스를 마이그레이션할 수 없습니다. Access 데이터베이스에서 작업 그룹 보호를 제거 하려면 다음 단계를 수행 합니다.  
  
1.  Access 데이터베이스 파일을 다른 위치로 복사 합니다.  
  
2.  복사 된 데이터베이스를 엽니다.  
  
3.  에 **도구** 메뉴에서 **보안**를 선택한 후 **사용자 및 그룹 권한**합니다.  
  
4.  선택를 **사용자** 옵션을 선택 합니다 **관리자** 사용자 있는지를 확인 합니다 **관리** 권한이 선택 됩니다.  
  
5.  선택는 **그룹** 옵션을 선택 합니다 **사용자** 그룹화 및 확인 한 다음를 **관리** 권한이 선택 됩니다.  
  
6.  클릭 **확인**를 선택한 다음는 **파일** 메뉴에서 클릭 **종료**합니다.  
  
복사 된 데이터베이스를 마이그레이션하려면 SSMA를 이제 사용할 수 있습니다. 스키마를 로드 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 데이터베이스에서 수동으로 보호할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
### <a name="backing-up-databases"></a>데이터베이스 백업  
액세스 하려면 데이터베이스를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 마이그레이션하는 경우 모두는 Access 데이터베이스를 백업 해야 뿐만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 마이그레이션하려는 데이터베이스 개체 및 데이터에 액세스 합니다.  
  
Access 데이터베이스를 백업 하는 **도구** 메뉴에서 **Database Utilities**를 선택한 후 **데이터베이스 백업**합니다.  
  
백업 하는 방법에 대 한 자세한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 참조 하세요. "백업에서 데이터베이스 및 복원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
### <a name="documenting-databases"></a>데이터베이스 문서화  
데이터베이스 개체, 파일 크기 및 사용 권한과 액세스 데이터베이스의 목록과 같은 속성을 문서화할 수도 있습니다. Access에서이 문서에서 생성 하는 **도구** 메뉴에서 **분석**를 클릭 하 고 **문서화**합니다.  
  
## <a name="see-also"></a>참고자료  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[SQL Server에 대 한 액세스 응용 프로그램 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)

---
title: 마이그레이션을 위해 Access 데이터베이스 준비 (AccessToSQL) | Microsoft Docs
description: SQL Server 또는 Azure SQL Database로 마이그레이션할 Access 데이터베이스를 결정 하 고 해당 데이터베이스를 마이그레이션할 준비가 되었는지 확인 하는 방법을 알아봅니다.
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
ms.openlocfilehash: 1b0fe1ef2f51da9e64954040e58440a9e7eee58e
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293728"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>마이그레이션을 위해 Access 데이터베이스 준비 (AccessToSQL)
Access 데이터베이스를로 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션할 데이터베이스를 결정 하 고 해당 데이터베이스를 마이그레이션할 준비가 되었는지 확인 해야 합니다.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>SQL Server로 마이그레이션할 시기 결정  
액세스를 위한 데이터베이스 엔진으로 사용 되는 Jet 데이터베이스 엔진은 데이터 관리를 위한 유연 하 고 사용 하기 쉬운 솔루션입니다. 그러나 데이터베이스가 커지고 업무에 중요 한 영향을 받을 수 있으므로 많은 사용자가 더 높은 성능, 보안 또는 가용성을 요구 하는 것을 알게 됩니다. 더 강력한 데이터 플랫폼이 필요한 응용 프로그램의 경우 해당 응용 프로그램에 대 한 기본 데이터베이스를로 이동 하는 것이 좋습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 마이그레이션 시기를 결정 하는 방법에 대 한 자세한 내용은 웹 사이트의 [마이그레이션 정보 페이지](https://go.microsoft.com/fwlink/?LinkId=68571) 를 참조 하십시오 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
로 데이터베이스를 마이그레이션한 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 된 테이블을 사용 하 여 계속 액세스를 사용 하거나 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 와 직접 상호 작용 하는 .NET Framework 기반 코드로 응용 프로그램을 수동으로 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="determining-which-databases-to-migrate"></a>마이그레이션할 데이터베이스 결정  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access 용 SSMA (Migration Assistant)는 Access 데이터베이스를 찾을 수 있습니다. 그런 다음 해당 데이터베이스에 대 한 메타 데이터를로 내보낼 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 메타 데이터를 내보내고 쿼리 하는 방법에 대 한 자세한 내용은 [액세스 인벤토리 내보내기](exporting-an-access-inventory-accesstosql.md)를 참조 하세요.  

   > [!NOTE]
   > 모든 액세스 기능 및 설정이에서 지원 되는 것은 아닙니다. 또는로 쉽게 변환할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 데이터베이스 마이그레이션을 시작 하기 전에 [호환 되지 않는 액세스 기능](incompatible-access-features-accesstosql.md)을 참조 하세요.
  
## <a name="preparing-for-migration"></a>마이그레이션 준비  
로의 마이그레이션을 위해 Access 데이터베이스를 준비 하려면 다음 지침을 따르십시오 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="upgrading-older-access-databases"></a>이전 Access 데이터베이스 업그레이드  
Access 용 SSMA는 97 이상 버전에 대 한 액세스를 지원 합니다. 이전 버전의 Access에서 데이터베이스를 사용 하는 경우 데이터베이스를 열고 Access 97 이상 버전에서 저장 합니다.  
  
### <a name="removing-workgroup-protection"></a>작업 그룹 보호 제거  
SSMA는 작업 그룹 보호를 사용 하는 데이터베이스를 마이그레이션할 수 없습니다. Access 데이터베이스에서 작업 그룹 보호를 제거 하려면 다음 단계를 수행 합니다.  
  
1.  Access 데이터베이스 파일을 다른 위치에 복사 합니다.  
  
2.  복사한 데이터베이스를 엽니다.  
  
3.  **도구** 메뉴에서 **보안**을 가리킨 다음 **사용자 및 그룹 권한**을 선택 합니다.  
  
4.  **사용자** 옵션을 선택 하 고 **관리** 사용자를 선택한 다음 **관리** 권한이 선택 되어 있는지 확인 합니다.  
  
5.  **그룹** 옵션을 선택 하 고 **사용자** 그룹을 선택한 다음 **관리** 권한이 선택 되어 있는지 확인 합니다.  
  
6.  **확인**을 클릭 한 다음 **파일** 메뉴에서 **끝내기**를 클릭 합니다.  
  
이제 SSMA를 사용 하 여 복사 된 데이터베이스를 마이그레이션할 수 있습니다. 에 스키마를 로드 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는에서 데이터베이스를 수동으로 보호할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="backing-up-databases"></a>데이터베이스 백업  
Access 데이터베이스를로 마이그레이션하기 전에 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] access 데이터베이스 뿐만 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 개체와 데이터를 마이그레이션할 데이터베이스를 모두 백업 해야 합니다.  
  
Access 데이터베이스를 백업 하려면 **도구** 메뉴에서 **데이터베이스 유틸리티**를 가리킨 다음 **데이터베이스 백업**을 선택 합니다.  
  
데이터베이스를 백업 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "의 데이터베이스 백업 및 복원"을 참조 하십시오 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="documenting-databases"></a>데이터베이스 문서화  
Access 데이터베이스의 데이터베이스 개체 목록, 파일 크기, 권한 등의 속성을 문서화할 수도 있습니다. Access에서이 설명서를 생성 하려면 **도구** 메뉴에서 **분석**을 가리킨 다음 **문서화**를 클릭 합니다.  
  
## <a name="see-also"></a>참조  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[SQL Server에 액세스 응용 프로그램 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)

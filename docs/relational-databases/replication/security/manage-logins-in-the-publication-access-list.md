---
title: 게시 액세스 목록에서 로그인 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- logins [SQL Server replication], managing
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6ff9fece0d1cb995e0d1643bf41bd095f7fe6bf5
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923645"
---
# <a name="manage-logins-in-the-publication-access-list"></a>게시 액세스 목록에서 로그인 관리
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 게시 액세스 목록의 로그인을 관리하는 방법에 대해 설명합니다. 게시에 대한 액세스는 PAL(게시 액세스 목록)에서 제어합니다. 로그인 및 그룹을 추가하고 PAL에서 제거할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
-   **다음을 사용하여 게시 액세스 목록에서 로그인을 관리하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   PAL에 로그인을 추가하려면 먼저 게시 데이터베이스의 데이터베이스 사용자와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 연결해야 합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **게시 속성 - \<Publication>** 대화 상자의 **게시 액세스 목록** 페이지에서 PAL(게시 액세스 목록)을 사용하여 로그인을 관리할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-manage-logins-in-the-pal"></a>PAL에서 로그인을 관리하려면  
  
1.  **게시 속성 - \<Publication>** 대화 상자의 **게시 액세스 목록** 페이지에서 **추가**, **제거** 및 **모두 제거** 단추를 사용하여 PAL에서 로그인과 그룹을 추가 및 제거합니다. PAL에서 **distributor_admin** 은 제거하지 마세요. 이 계정은 복제에 사용됩니다.  
  
    > [!NOTE]  
    >  원격 배포자를 사용할 경우 PAL의 계정을 게시자와 배포자에서 모두 사용할 수 있어야 합니다. 이 계정은 두 서버 모두에 정의된 도메인 계정이나 로컬 계정이어야 합니다. 또한 두 로그인과 연결된 암호는 같아야 합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-groups-and-logins-that-belong-to-the-pal"></a>PAL에 속한 그룹 및 로그인을 보려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_help_publication_access](../../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)를 실행합니다. 이때 `@publication`에 게시 이름을 지정합니다. 그러면 PAL의 그룹 및 로그인에 대한 정보가 표시됩니다.  
  
#### <a name="to-add-groups-and-logins-to-the-pal"></a>PAL에 그룹 및 로그인을 추가하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_grant_publication_access](../../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)를 실행합니다. 이때 `@publication`에 게시 이름, `@login`에 추가되는 로그인 또는 그룹의 이름을 지정합니다.  
  
#### <a name="to-remove-groups-and-logins-from-the-pal"></a>PAL에서 그룹 및 로그인을 제거하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_revoke_publication_access](../../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)를 실행합니다. 이때 `@publication`에 게시 이름, `@login`에 제거되는 로그인 또는 그룹의 이름을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 액세스 목록에서 로그인 관리](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)   
 [복제 에이전트 보안 모델](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [복제 토폴로지 보안 설정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [게시자 보안 설정](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  

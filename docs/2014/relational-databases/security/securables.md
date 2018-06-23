---
title: 보안 개체 | Microsoft 문서
ms.custom: ''
ms.date: 10/14/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.roleproperties.selectobject.f1
helpviewer_keywords:
- securables [SQL Server]
- schemas [SQL Server], securables
- database securables [SQL Server]
- hierarchies [SQL Server], securables
- server securables [SQL Server]
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b2679a2583b21ba1015b9b54e5e1662c9e89bf5d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187373"
---
# <a name="securables"></a>보안 개체
  보안 개체는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인증 시스템이 액세스를 조정하는 리소스입니다. 예를 들어, 테이블은 보안 개체입니다. 스스로 보호할 수 있는 "범위"라는 중첩된 계층을 만들면 일부 보안 개체를 다른 보안 개체에 포함시킬 수 있습니다. 보안 개체 범위는 **서버**, **데이터베이스**및 **스키마**입니다.  
  
## <a name="securable-scope-server"></a>보안 개체 범위: 서버  
 **서버** 보안 개체 범위는 다음 보안 개체를 포함합니다.  
  
-   가용성 그룹  
  
-   끝점  
  
-   로그인  
  
-   서버 역할  
  
-   데이터베이스  
  
## <a name="securable-scope-database"></a>보안 개체 범위: 데이터베이스  
 **데이터베이스** 보안 개체 범위는 다음 보안 개체를 포함합니다.  
  
-   응용 프로그램 역할  
  
-   어셈블리  
  
-   비대칭 키  
  
-   인증서  
  
-   계약  
  
-   전체 텍스트 카탈로그  
  
-   전체 텍스트 중지 목록  
  
-   메시지 유형  
  
-   원격 서비스 바인딩  
  
-   (데이터베이스) 역할  
  
-   경로  
  
-   스키마  
  
-   검색 속성 목록  
  
-   서비스  
  
-   대칭 키  
  
-   사용자  
  
## <a name="securable-scope-schema"></a>보안 개체 범위: 스키마  
 **스키마** 보안 개체 범위는 다음 보안 개체를 포함합니다.  
  
-   형식  
  
-   XML 스키마 컬렉션  
  
-   개체 - 개체 클래스 멤버는 다음과 같습니다.  
  
    -   집계  
  
    -   기능  
  
    -   프로시저  
  
    -   큐  
  
    -   동의어  
  
    -   Table  
  
    -   보기  
  
## <a name="controlling-access-to-a-securable"></a>보안 개체에 대한 액세스 제어  
 보안 개체에 대한 사용 권한을 받는 엔터티를 주체라고 합니다. 가장 일반적인 보안 주체는 로그인 및 데이터베이스 사용자입니다. 사용 권한을 부여 또는 거부하거나, 액세스 권한이 있는 역할에 로그인 및 사용자를 추가하여 보안 개체에 대한 액세스를 제어합니다. 사용 권한을 제어하는 방법은 [GRANT&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql), [REVOKE&#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql), [DENY&#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql), [sp_addrolemember&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) 및 [sp_droprolemember&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)입니다.  
  
> [!CAUTION]  
>  설치 시 시스템 개체에 부여되는 기본 사용 권한은 발생할 수 있는 위협이 있는지 신중하게 평가되며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 보안 강화의 일환으로 변경할 필요는 없습니다. 시스템 개체에 대한 사용 권한을 변경하면 기능이 제한 또는 중단될 수 있으며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치가 지원되지 않는 상태가 될 수 있습니다.  
  
## <a name="related-content"></a>관련 내용  
 [SQL Server 보안 설정](securing-sql-server.md)  
  
 [sys.database_principals&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)  
  
 [sys.database_role_members&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)  
  
 [sys.server_principals&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)  
  
 [sys.server_role_members&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)  
  
 [sys.sql_logins&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)  
  
  

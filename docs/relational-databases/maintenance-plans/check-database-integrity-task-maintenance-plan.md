---
title: 데이터베이스 무결성 검사 태스크(유지 관리 계획) | Microsoft 문서
description: 데이터베이스 무결성 검사 태스크를 사용하여 SQL Server 데이터베이스에서 사용자 및 시스템 테이블과 인덱스의 할당 및 구조적 무결성을 검사합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.maintplanproperties.integrity.f1
- sql13.swb.maint.integrity.f1
helpviewer_keywords:
- Check Database Integrity Task dialog box
ms.assetid: 3534494a-5dfe-4738-b49a-e7fabd731c47
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a833b67471ad05e45f54776d49ec529c7fbb6fb5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85667867"
---
# <a name="check-database-integrity-task-maintenance-plan"></a>데이터베이스 무결성 검사 태스크(유지 관리 계획)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **데이터베이스 무결성 검사 태스크** 대화 상자를 사용하면 `DBCC CHECKDB`[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 사용자 및 시스템 테이블, 데이터베이스 인덱스의 할당 및 구조적 무결성을 검사할 수 있습니다. `DBCC` 를 실행하면 데이터베이스의 모든 무결성 문제가 보고되므로 시스템 관리자나 데이터베이스 소유자가 나중에 이 문제들을 처리할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **연결**  
 이 태스크를 수행할 때 사용할 서버 연결을 선택합니다.  
  
 **새로 만들기**  
 이 태스크를 수행할 때 사용할 새 서버 연결을 만듭니다. 아래에서는 **새 연결** 대화 상자에 대해 설명합니다.  
  
 **데이터베이스**  
 이 태스크의 영향을 받는 데이터베이스를 지정합니다.  
  
-   **모든 데이터베이스**  
  
     **tempdb**를 제외한 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다.  
  
-   **모든 시스템 데이터베이스**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tempdb **를 제외한 각**시스템 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 사용자가 만든 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
-   **모든 사용자 데이터베이스**  
  
     사용자가 만든 모든 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
-   **다음 데이터베이스**  
  
     선택한 데이터베이스에 대해서만 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 이 옵션을 선택한 경우에는 목록에서 하나 이상의 데이터베이스를 선택해야 합니다.  
  
    > [!NOTE]  
    >  유지 관리 계획은 호환성 수준 80 이상으로 설정된 데이터베이스에 대해서만 실행합니다. 호환성 수준 70 이하로 설정된 데이터베이스는 표시되지 않습니다.  
  
 **인덱스 포함**  
 모든 인덱스 페이지와 테이블 데이터 페이지가 올바른지 확인합니다.  
  
 **Physical only**  
 페이지와 레코더 헤더의 물리적 구조 무결성과 데이터베이스 할당 일관성만 검사합니다. 이 옵션을 사용하여 대형 데이터베이스에서 DBCC CHECKDB 실행 시간을 줄일 수 있으므로 프로덕션 시스템에서 검사를 자주 수행할 때는 이 옵션을 사용하는 것이 좋습니다.  
  
 **TABLOCK**  
 내부 데이터베이스 스냅샷을 사용하는 대신 DBCC CHECKDB가 잠금을 가져오도록 합니다. 여기에는 데이터베이스에 대한 단기 배타(X) 잠금이 포함됩니다. 이 옵션을 사용하면 데이터베이스 로드가 많은 상황에서 DBCC CHECKDB가 더 빠르게 실행됩니다. 그러나 DBCC CHECKDB가 실행되는 동안 데이터베이스의 동시 사용 가능성은 줄어듭니다.  
  
 **T-SQL 보기**  
 선택한 옵션을 기반으로 서버에 대해 수행한 이 태스크의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 표시합니다.  
  
> [!NOTE]  
>  영향을 받은 개체 수가 많은 경우에는 표시하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="new-connection-dialog-box"></a>새 연결 대화 상자  
 **연결 이름**  
 새 연결의 이름을 입력합니다.  
  
 **서버 이름 선택 또는 입력**  
 이 태스크를 수행할 때 연결할 서버를 선택합니다.  
  
 **새로 고침**  
 사용할 수 있는 서버 목록을 새로 고칩니다.  
  
 **서버 로그온 정보 입력**  
 서버에 대한 인증 방법을 지정합니다.  
  
 **Windows NT 통합 보안 사용**  
 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.  
  
 **특정 사용자 이름 및 암호 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다. 이 옵션은 사용할 수 없습니다.  
  
 **사용자 이름**  
 인증 시 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
 **암호**  
 인증 시 사용할 암호를 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
  

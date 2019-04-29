---
title: 통계 업데이트 태스크(유지 관리 계획) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.statistics.f1
helpviewer_keywords:
- Updates Statistics Task dialog box
ms.assetid: 22902fd0-eb39-4f18-af94-3fcb69d2a3a4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 51a3deffc9db182f7b3ad8f50d27c24e0f74dc6d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807118"
---
# <a name="update-statistics-task-maintenance-plan"></a>통계 업데이트 태스크(유지 관리 계획)
   **통계 업데이트 태스크** 대화 상자를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 테이블 및 인덱스 데이터 정보를 업데이트할 수 있습니다. 데이터베이스의 사용자 테이블에 작성된 각 인덱스의 배포 통계를 다시 샘플링합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용하는 배포 통계는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 처리하는 동안 테이블 탐색을 최적화합니다. 배포 통계를 자동으로 구축하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 각 인덱스에 대한 해당 테이블에서 데이터를 주기적으로 샘플링합니다. 샘플링하는 양은 테이블의 행 수와 데이터 수정 빈도를 기초로 정해집니다. 테이블에서 지정한 비율의 데이터를 사용하여 추가 샘플링을 수행하려면 이 옵션을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 이 정보를 사용하여 보다 향상된 쿼리 계획을 만듭니다.  
  
 이 태스크는 UPDATE STATISTICS 문을 실행합니다.  
  
## <a name="options"></a>변수  
 **대량 삽입 태스크 편집기**  
 이 태스크를 수행할 때 사용할 서버 연결을 선택합니다.  
  
 **새로 만들기**  
 이 태스크를 수행할 때 사용할 새 서버 연결을 만듭니다. 아래에서는 **새 연결** 대화 상자에 대해 설명합니다.  
  
 **데이터베이스**  
 이 태스크의 영향을 받는 데이터베이스를 지정합니다.  
  
-   **모든 데이터베이스**  
  
     tempdb를 제외한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다.  
  
-   **모든 시스템 데이터베이스**  
  
     tempdb를 제외한 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 사용자가 만든 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
-   **모든 사용자 데이터베이스**  
  
     사용자가 만든 모든 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
-   **다음 데이터베이스**  
  
     선택한 데이터베이스에 대해서만 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 이 옵션을 선택한 경우에는 목록에서 하나 이상의 데이터베이스를 선택해야 합니다.  
  
 **참고** 유지 관리 계획은 호환성 수준 80 이상으로 설정된 데이터베이스에 대해서만 실행합니다. 호환성 수준 70 이하로 설정된 데이터베이스는 표시되지 않습니다.  
  
 **개체**  
 테이블, 뷰 또는 둘 다를 표시하도록 **선택** 표를 제한합니다.  
  
 **선택**  
 이 태스크의 영향을 받는 테이블 또는 인덱스를 지정합니다. 개체 상자에서 **테이블 및 뷰** 를 선택한 경우에는 사용할 수 없습니다.  
  
 **모든 기존 통계**  
 열과 인덱스의 통계를 모두 업데이트합니다.  
  
 **열 통계만**  
 열 통계만 업데이트합니다.  
  
 **인덱스 통계만**  
 인덱스 통계만 업데이트합니다.  
  
 **검색 유형**  
 업데이트된 통계를 수집하는 데 사용되는 검색 유형입니다.  
  
 **전체 검색**  
 통계를 수집하기 위해 테이블이나 뷰의 모든 행을 읽습니다.  
  
 **샘플링 기준**  
 보다 큰 테이블이나 뷰에 대한 통계를 수집할 때 샘플링할 행의 수 또는 테이블이나 인덱싱된 뷰의 백분율을 지정합니다.  
  
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
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인스턴스에 연결합니다.  
  
 **특정 사용자 이름 및 암호 사용**  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다. 이 옵션은 사용할 수 없습니다.  
  
 **사용자 이름**  
 인증 시 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
 **암호**  
 인증 시 사용할 암호를 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)  
  
  

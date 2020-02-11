---
title: '자습서: Transact-SQL 문 작성 | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL statements, tutorials
- Transact-SQL tutorials
- tutorials [Transact-SQL]
ms.assetid: 2addc9be-67d0-423d-a457-192fe9d7d058
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 67e09713fdec72313bde6ba81e1cc169467fda0c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211193"
---
# <a name="tutorial-writing-transact-sql-statements"></a>자습서: Transact-SQL 문 작성
  [!INCLUDE[tsql](../includes/tsql-md.md)] 문 작성 자습서를 시작합니다. 이 자습서는 SQL 문을 처음 작성하는 사용자를 위해 제공됩니다. 이 자습서는 새로운 사용자가 테이블을 만들고 데이터를 삽입하는 몇 가지 기본 문을 통해 작업을 시작하는 데 도움이 될 것입니다. 이 자습서에서는 [!INCLUDE[tsql](../includes/tsql-md.md)]가 구현하는 SQL 표준인 [!INCLUDE[msCoName](../includes/msconame-md.md)] 을 사용합니다. 이 자습서는 [!INCLUDE[tsql](../includes/tsql-md.md)] 클래스를 대체하는 것이 아니라 [!INCLUDE[tsql](../includes/tsql-md.md)] 언어를 간략하게 소개하는 데 목적이 있습니다. 의도적으로 간단한 문을 이 자습서에서 사용하고 있으므로 일반적인 프로덕션 데이터베이스에서 볼 수 있는 복잡한 문은 다루지 않습니다.  
  
> [!NOTE]  
>  일반적으로 데이터베이스 초보 사용자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 문을 작성하는 것보다 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)]에서 작업하는 것이 더 간편할 것입니다.  
  
## <a name="finding-more-information"></a>추가 정보 찾기  
 특정 문에 대한 자세한 내용을 보려면 SQL Server 온라인 설명서에 이름으로 해당 문을 검색하거나 목차를 사용하여 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](/sql/t-sql/language-reference) 아래에 사전순으로 나열된 1,800개의 언어 요소를 찾아봅니다. 또한 관심이 있는 주제와 관련된 키워드를 검색하는 것도 좋은 방법이 될 수 있습니다. 예를 들어 월과 같은 날짜의 일부를 반환하는 방법을 보려면 **dates [SQL Server]** 의 색인을 검색한 다음 **dateparts**를 선택합니다. 이렇게 하면 [DATEPART&#40;Transact-SQL&#41;](/sql/t-sql/functions/datepart-transact-sql) 항목이 제공됩니다. 마찬가지로 문자열을 사용하는 방법을 보려면 **문자열 함수**를 검색합니다. 이렇게 하면 [문자열 함수&#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql) 항목이 제공됩니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 데이터베이스 작성, 데이터베이스에서 테이블 작성, 테이블에 데이터 삽입, 데이터 업데이트, 데이터 읽기, 데이터 삭제, 테이블 삭제 등을 수행하는 방법을 보여 줍니다. 뷰와 저장 프로시저를 만들고 데이터베이스 및 데이터에 대해 사용자를 구성합니다.  
  
 이 자습서는 다음 3개의 단원으로 이루어져 있습니다.  
  
 [1단원: 데이터베이스 개체 만들기](lesson-1-creating-database-objects.md)  
 이 단원에서는 데이터베이스 작성, 데이터베이스에서 테이블 작성, 테이블에 데이터 삽입, 데이터 업데이트, 데이터 읽기 등을 수행합니다.  
  
 [2단원: 데이터베이스 개체에 대한 사용 권한 구성](lesson-2-configuring-permissions-on-database-objects.md)  
 이 단원에서는 로그인 및 사용자를 만듭니다. 또한 뷰와 저장 프로시저를 만든 다음 저장 프로시저에 대한 사용 권한을 사용자에게 부여합니다.  
  
 [3단원: 데이터베이스 개체에 대한 액세스 권한 부여](lesson-3-1-deleting-database-objects.md)  
 이 단원에서는 데이터 액세스 권한 제거, 테이블에서 데이터 삭제, 테이블 삭제, 데이터베이스 삭제 등을 수행합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 자습서를 완료하려면 SQL 언어를 알 필요가 없지만 테이블과 같은 기본 데이터베이스 개념을 이해해야 합니다. 이 자습서를 진행하는 동안 데이터베이스를 만들고 Windows 사용자를 만듭니다. 이러한 태스크를 수행하려면 높은 수준의 사용 권한이 필요하므로 컴퓨터에 관리자로 로그인해야 합니다.  
  
 시스템에는 다음이 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)](버전은 관계 없음)  
  
-   
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 또는 Management Studio Express  
  
-   Internet Explorer 6 이상  
  
> [!NOTE]  
>  자습서를 검토할 때는 문서 뷰어 도구 모음에 **다음** 단추 및 **이전** 단추를 추가 하는 것이 좋습니다.  
  
  

---
title: 데이터베이스 엔진 튜닝 관리자 시작 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tuning databases [SQL Server]
- Database Engine Tuning Advisor [SQL Server], starting
ms.assetid: 4abc0e10-96fd-4e46-93d6-d7ee03eec844
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed2001ff159681f78a9287be8e1931ee5d432948
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282289"
---
# <a name="launching-database-engine-tuning-advisor"></a>데이터베이스 엔진 튜닝 관리자 시작
  시작하려면 데이터베이스 엔진 튜닝 관리자 GUI(그래픽 사용자 인터페이스)를 엽니다. 처음 사용할 때는 **sysadmin** 고정 서버 역할의 멤버가 데이터베이스 엔진 튜닝 관리자를 시작하여 응용 프로그램을 초기화해야 합니다. 초기화 후에는 **db_owner** 고정 데이터베이스 역할의 멤버가 데이터베이스 엔진 튜닝 관리자를 사용하여 자신이 소유한 데이터베이스를 튜닝할 수 있습니다. 데이터베이스 엔진 튜닝 관리자를 초기화하는 방법은 [데이터베이스 엔진 튜닝 관리자 시작 및 사용](../../relational-databases/performance/database-engine-tuning-advisor.md)을 참조하세요.  
  
### <a name="open-the-database-engine-tuning-advisor-gui"></a>데이터베이스 엔진 튜닝 관리자 GUI 열기  
  
1.  Windows **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **성능 도구**를 차례로 가리킨 다음 **데이터베이스 엔진 튜닝 관리자**를 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서 기본 설정을 확인한 다음 **연결**을 클릭합니다.  
  
 기본적으로 데이터베이스 엔진 튜닝 관리자는 다음 그림에 있는 구성으로 열립니다.  
  
 ![데이터베이스 엔진 튜닝 관리자 기본 창](media/defaultdtagui.gif "데이터베이스 엔진 튜닝 관리자 기본 창")  
  
> [!NOTE]  
>  탭 및 **세션 이름** 상자에 컴퓨터 이름과 연결하려는 인스턴스가 표시됩니다. 탭과 상자에는 현재 날짜 및 시간도 표시됩니다.  
  
 데이터베이스 엔진 튜닝 관리자 GUI를 처음 열면 두 개의 주 창이 표시됩니다.  
  
-   왼쪽 창에는 이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 수행된 튜닝 세션을 모두 나열하는 세션 모니터가 있습니다. 데이터베이스 엔진 튜닝 관리자를 열면 이 창 상단에 새 세션이 표시됩니다. 인접한 창에서 이 세션의 이름을 지정할 수 있습니다. 처음에는 기본 세션만 나열됩니다. 이 세션은 데이터베이스 엔진 튜닝 관리자에서 자동으로 만드는 기본 세션입니다. 데이터베이스를 튜닝한 후에는 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 튜닝 세션이 새 세션 아래에 나열됩니다. 튜닝 세션을 마우스 오른쪽 단추로 클릭하여 이름을 바꾸거나 닫거나 삭제하거나 복제할 수 있습니다. 목록에서 마우스 오른쪽 단추를 클릭하면 이름, 상태 또는 만든 날짜를 기준으로 세션을 정렬하거나 새 세션을 만들 수 있습니다. 이 창 하단에는 선택한 튜닝 세션의 세부 정보가 표시됩니다. **항목별** 단추를 사용하여 세부 정보를 범주별로 정리해서 표시하거나 **사전순** 단추를 사용하여 사전순으로 정렬된 목록으로 표시할 수 있습니다. 오른쪽 창 테두리를 창의 왼쪽으로 끌어서 세션 모니터를 숨길 수도 있습니다. 다시 표시하려면 창 테두리를 오른쪽으로 다시 끕니다. 세션 모니터를 사용하면 이전 튜닝 세션을 보거나 이전 튜닝 세션으로 비슷한 정의가 있는 새 세션을 만들 수 있습니다. 세션 모니터를 사용하여 튜닝 권장 구성을 평가할 수도 있습니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)을 참조하세요. 브라우저의 **뒤로** 단추를 사용하여 이 자습서로 돌아올 수 있습니다.  
  
-   오른쪽 창에는 **일반** 탭과 **튜닝 옵션** 탭이 있습니다. 이 창에서는 데이터베이스 엔진 튜닝 세션을 정의할 수 있습니다. **일반** 탭에서는 튜닝 세션의 이름을 입력하고 사용할 작업 파일이나 테이블을 지정하며 이 세션에서 튜닝할 데이터베이스와 테이블을 선택합니다. 작업은 튜닝하려는 데이터베이스에 대해 실행되는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. 데이터베이스 엔진 튜닝 관리자에서는 데이터베이스를 튜닝할 때 추적 파일, 추적 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 또는 XML 파일을 작업 입력으로 사용합니다. **튜닝 옵션** 탭에서는 데이터베이스 엔진 튜닝 관리자에서 분석하는 동안 고려할 물리적 데이터베이스 디자인 구조(인덱스 또는 인덱싱된 뷰)와 분할 전략을 선택할 수 있습니다. 이 탭에서는 데이터베이스 엔진 튜닝 관리자에서 작업을 튜닝하는 데 걸리는 최대 시간을 지정할 수도 있습니다. 기본적으로 데이터베이스 엔진 튜닝 관리자에서는 한 시간 동안 작업을 튜닝합니다.  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 편집기에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 스크립트를 가져올 때 데이터베이스 엔진 튜닝 관리자에서 XML 파일을 입력으로 사용할 수 있습니다. 자세한 내용은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 데이터베이스 엔진 튜닝 관리자 시작 및 사용 [의](../../relational-databases/performance/database-engine-tuning-advisor.md)쿼리 편집기에서 데이터베이스 엔진 튜닝 관리자 시작에 대한 섹션을 참조하세요.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [도구 옵션 및 레이아웃 설정](lesson-1-2-setting-tool-options-and-layout.md)  
  
  

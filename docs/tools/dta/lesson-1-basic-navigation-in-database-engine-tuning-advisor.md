---
title: '1단원: 데이터베이스 엔진 튜닝 관리자 기본 탐색 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
ms.assetid: ad49b2e0-a5e3-49d2-80fd-9f4eaa3652cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ee0b1c221c3bdb18ec9b79339e9dd55cb4eed93e
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49071807"
---
# <a name="lesson-1-basic-navigation-in-database-engine-tuning-advisor"></a>1단원: 데이터베이스 엔진 튜닝 관리자 기본 탐색
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
데이터베이스 엔진 튜닝 관리자를 사용하면 GUI(그래픽 사용자 인터페이스)를 기반으로 튜닝 세션과 튜닝 권장 구성 보고서를 볼 수 있습니다. 이 단원에서는 도구를 시작하는 방법과 도구 화면을 구성하는 방법을 보여 줍니다. 이 세션의 작업을 마치면 도구를 시작하는 여러 방법과 정기적으로 수행하는 튜닝 태스크를 지원하도록 도구 화면을 구성하는 방법을 알게 됩니다.  

## <a name="prerequisites"></a>사전 요구 사항 

이 자습서를 완료하려면 SQL Server Management Studio, SQL Server를 실행하는 서버에 대한 액세스 및 AdventureWorks 데이터베이스가 필요합니다.

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks2017 샘플 데이터베이스](https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017)를 다운로드합니다.


SSMS에서 데이터베이스를 복원하기 위한 지침은 [데이터베이스 복원](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017)을 참조하세요.

  >[!NOTE]
  > 이 자습서는 기본적인 데이터베이스 관리 작업 및 SQL Server Management Studio를 사용 하 여 친숙 한 사용자에 대 한 것입니다. 
  

## <a name="launch-database-tuning-advisor"></a>데이터베이스 튜닝 관리자 시작 
시작하려면 DTA(데이터베이스 엔진 튜닝 관리자) GUI(그래픽 사용자 인터페이스)를 엽니다. 처음 사용할 때는 **sysadmin** 고정 서버 역할의 멤버가 데이터베이스 엔진 튜닝 관리자를 시작하여 응용 프로그램을 초기화해야 합니다. 초기화 후에는 **db_owner** 고정 데이터베이스 역할의 멤버가 데이터베이스 엔진 튜닝 관리자를 사용하여 자신이 소유한 데이터베이스를 튜닝할 수 있습니다. 데이터베이스 엔진 튜닝 관리자를 초기화하는 방법은 [데이터베이스 엔진 튜닝 관리자 시작 및 사용](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
1. SSMS(SQL Server Management Studio)를 시작합니다. Windows에서 **시작 메뉴**, 가리킨 **프로그램도** 찾아서 **SQL Server Management Studio**. 
2. SSMS 열기를 선택 합니다 **도구** 선택한 메뉴 **데이터베이스 튜닝**합니다. 

  ![SSMS에서 DTA를 실행 합니다.](media/dta-tutorials/launch-dta.png)

3. 데이터베이스 튜닝 관리자 시작 하 고 엽니다는 **서버에 연결** 대화 상자. 기본 설정을 확인 하 고 선택한 **Connect** SQL Server에 연결 합니다.  
  
기본적으로 데이터베이스 엔진 튜닝 관리자는 다음 그림에 있는 구성으로 열립니다.  
  
![데이터베이스 엔진 튜닝 관리자 기본 창](media/dta-tutorials/dta-default-gui.png)
  
> [!NOTE]  
> 합니다 **세션 모니터** 탭에는 연결 된 사용자 및 현재 데이터의 이름인 세션 이름을 표시 합니다. 
  
데이터베이스 엔진 튜닝 관리자 GUI를 처음 열면 두 개의 주 창이 표시됩니다.  
  
-   왼쪽 창에는 이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 수행된 튜닝 세션을 모두 나열하는 세션 모니터가 있습니다. 데이터베이스 엔진 튜닝 관리자를 열면 이 창 상단에 새 세션이 표시됩니다. 인접한 창에서 이 세션의 이름을 지정할 수 있습니다. 처음에는 기본 세션만 나열됩니다. 이 세션은 데이터베이스 엔진 튜닝 관리자에서 자동으로 만드는 기본 세션입니다. 데이터베이스를 튜닝한 후에는 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 튜닝 세션이 새 세션 아래에 나열됩니다. 튜닝 세션을 마우스 오른쪽 단추로 클릭하여 이름을 바꾸거나 닫거나 삭제하거나 복제할 수 있습니다. 목록에서 마우스 오른쪽 단추를 클릭하면 이름, 상태 또는 만든 날짜를 기준으로 세션을 정렬하거나 새 세션을 만들 수 있습니다. 이 창 하단에는 선택한 튜닝 세션의 세부 정보가 표시됩니다. **항목별** 단추를 사용하여 세부 정보를 범주별로 정리해서 표시하거나 **사전순** 단추를 사용하여 사전순으로 정렬된 목록으로 표시할 수 있습니다. 오른쪽 창 테두리를 창의 왼쪽으로 끌어서 세션 모니터를 숨길 수도 있습니다. 다시 표시하려면 창 테두리를 오른쪽으로 다시 끕니다. 세션 모니터를 사용하면 이전 튜닝 세션을 보거나 이전 튜닝 세션으로 비슷한 정의가 있는 새 세션을 만들 수 있습니다. 세션 모니터를 사용하여 튜닝 권장 구성을 평가할 수도 있습니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)을 참조하세요. 브라우저의 **뒤로** 단추를 사용하여 이 자습서로 돌아올 수 있습니다.  
  
-   오른쪽 창에는 **일반** 탭과 **튜닝 옵션** 탭이 있습니다. 이 창에서는 데이터베이스 엔진 튜닝 세션을 정의할 수 있습니다. **일반** 탭에서는 튜닝 세션의 이름을 입력하고 사용할 작업 파일이나 테이블을 지정하며 이 세션에서 튜닝할 데이터베이스와 테이블을 선택합니다. 작업은 튜닝하려는 데이터베이스에 대해 실행되는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. 데이터베이스 엔진 튜닝 관리자에서는 데이터베이스를 튜닝할 때 추적 파일, 추적 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 또는 XML 파일을 작업 입력으로 사용합니다. **튜닝 옵션** 탭에서는 데이터베이스 엔진 튜닝 관리자에서 분석하는 동안 고려할 물리적 데이터베이스 디자인 구조(인덱스 또는 인덱싱된 뷰)와 분할 전략을 선택할 수 있습니다. 이 탭에서는 데이터베이스 엔진 튜닝 관리자에서 작업을 튜닝하는 데 걸리는 최대 시간을 튜닝할 수도 있습니다. 기본적으로 데이터베이스 엔진 튜닝 관리자에서는 한 시간 동안 작업을 튜닝합니다.  
  
> [!NOTE]  
> [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 편집기에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 스크립트를 가져올 때 데이터베이스 엔진 튜닝 관리자에서 XML 파일을 입력으로 사용할 수 있습니다. 자세한 내용은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 데이터베이스 엔진 튜닝 관리자 시작 및 사용 [의](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)쿼리 편집기에서 데이터베이스 엔진 튜닝 관리자 시작에 대한 섹션을 참조하세요.  
  
## <a name="configure-tool-options-and-layout"></a>도구 옵션 및 레이아웃을 구성 합니다. 

1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  

   ![DTA 옵션](media/dta-tutorials/dta-settings.png) 
  
2.  **옵션** 대화 상자에서 다음 옵션을 봅니다.  
  
    -   **시작 시** 목록을 확장하여 데이터베이스 엔진 튜닝 관리자를 시작할 때 표시될 수 있는 사항을 확인합니다. 기본적으로 **새 세션 표시** 가 선택되어 있습니다.  
  
    -   **글꼴 변경** 을 클릭하여 **일반** 탭의 데이터베이스 및 테이블 목록에 대해 선택할 수 있는 글꼴을 확인합니다. 이 옵션에 대해 선택한 글꼴은 튜닝을 수행한 후 데이터베이스 엔진 튜닝 관리자 권장 사항 표와 보고서에도 사용됩니다. 기본적으로 데이터베이스 엔진 튜닝 관리자에서는 시스템 글꼴을 사용합니다.  
  
    -   **가장 최근에 사용한 목록의 항목 수** 는 **1** 과 **10**사이에서 설정할 수 있습니다. 그러면 **파일** 메뉴에서 **최근에 사용한 세션** 이나 **최근에 사용한 파일** 을 클릭할 때 표시되는 목록의 최대 항목 수가 설정됩니다. 기본적으로 이 옵션은 **4**로 설정되어 있습니다.  
  
    -   **마지막 튜닝 옵션 저장** 을 선택하면 기본적으로 데이터베이스 엔진 튜닝 관리자에서 마지막 튜닝 세션에 대해 지정된 튜닝 옵션을 다음 튜닝 세션에 사용합니다. 데이터베이스 엔진 튜닝 관리자 옵션 기본값을 사용하려면 이 확인란의 선택을 취소합니다. 기본적으로 이 옵션은 선택되어 있습니다.  
  
    -   기본적으로 튜닝 세션을 실수로 삭제하지 않도록 **세션을 영구적으로 삭제하기 전에 확인** 이 선택되어 있습니다.  
  
    -   데이터베이스 엔진 튜닝 관리자가 작업 분석을 완료하기 전에 튜닝 세션을 실수로 중지하지 않도록 **세션 분석을 중지하기 전에 확인** 이 기본적으로 선택되어 있습니다.  
  
## <a name="next-lesson"></a>다음 단원  
[2단원: 데이터베이스 엔진 튜닝 관리자 사용](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
  
  
  

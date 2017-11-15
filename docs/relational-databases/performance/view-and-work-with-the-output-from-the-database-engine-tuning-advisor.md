---
title: "데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dta.sessionmonitor.f1
- sql13.dta.reports.f1
- sql13.dta.recommendations.f1
- sql13.dta.applyrecommendations.f1
helpviewer_keywords:
- viewing logs
- recommendations [Database Engine Tuning Advisor]
- summary tuning information [SQL Server]
- Database Engine Tuning Advisor [SQL Server], recommendations
- Database Engine Tuning Advisor [SQL Server], logs
- Database Engine Tuning Advisor [SQL Server], viewing output
- Database Engine Tuning Advisor [SQL Server], reports
- logs [SQL Server], tuning
- reports [SQL Server], tuning
- viewing tuning output
ms.assetid: 47f9d9a7-80b0-416d-9d9a-9e265bc190dc
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb34918a06fe49195766fbcdd22e8f762c9e4faf
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="view-and-work-with-the-output-from-the-database-engine-tuning-advisor"></a>데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 엔진 튜닝 관리자는 데이터베이스를 튜닝할 때 요약, 권장 구성, 보고서 및 튜닝 로그를 만듭니다. 튜닝 로그 출력을 사용하여 데이터베이스 엔진 튜닝 관리자 튜닝 세션의 문제를 해결할 수 있습니다. 요약, 권장 구성 및 보고서를 사용하여 튜닝 권장 구성을 구현하거나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 필요한 쿼리 성능이 향상될 때까지 튜닝을 계속합니다. 데이터베이스 튜닝 관리자를 사용하여 작업을 만들고 데이터베이스를 튜닝하는 방법은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
##  <a name="View"></a> 튜닝 출력 보기  
 다음 프로시저에서는 데이터베이스 엔진 튜닝 관리자 GUI로 튜닝 권장 구성, 요약, 보고서 및 튜닝 로그를 보는 방법에 대해 설명합니다. 사용자 인터페이스 옵션에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 [사용자 인터페이스 설명](#UI) 을 참조하세요.  
  
 GUI를 사용하여 **dta** 명령줄 유틸리티로 생성된 튜닝 출력을 볼 수도 있습니다.  
  
> [!NOTE]  
>  **dta** 명령줄 유틸리티를 사용하며 **-ox** 인수를 사용하여 XML 파일에 출력 내용이 기록되도록 지정하는 경우 **의** 파일 **메뉴에서** 파일 열기 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 클릭하여 XML 출력 파일을 열어 볼 수 있습니다. 자세한 내용은 [Use SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)을 참조하세요. **dta** 명령줄 유틸리티에 대한 자세한 내용은 [dta 유틸리티](../../tools/dta/dta-utility.md)를 참조하세요.  
  
#### <a name="to-view-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>데이터베이스 엔진 튜닝 관리자 GUI로 튜닝 권장 구성을 보려면  
  
1.  데이터베이스 엔진 튜닝 관리자 GUI 또는 **dta** 명령줄 유틸리티를 사용하여 데이터베이스를 튜닝합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 기존 튜닝 세션을 사용하려면 이 단계를 건너뛰고 2단계를 실행합니다.  
  
2.  데이터베이스 엔진 튜닝 관리자 GUI를 시작합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 기존 튜닝 세션의 튜닝 권장 구성을 보려면 **세션 모니터**창의 세션 이름을 두 번 클릭하여 세션을 엽니다.  
  
     새 튜닝 세션이 완료되거나 도구가 기존 세션을 로드한 후에 **권장 구성** 페이지가 표시됩니다.  
  
3.  **권장 구성** 페이지에서 **파티션 권장 구성** 및 **인덱스 권장 구성** 을 클릭하여 튜닝 세션 결과를 표시하는 창을 봅니다. 이 세션의 튜닝 옵션을 설정할 때 분할을 지정하지 않았다면 **파티션 권장 구성** 창이 비어 있습니다.  
  
4.  **파티션 권장 구성** 또는 **인덱스 권장 구성** 창에서 스크롤 막대를 사용하여 표에 표시된 모든 정보를 볼 수 있습니다.  
  
5.  **권장 구성** 탭 페이지의 아래쪽에 있는 **기존 개체 표시** 의 선택을 해제합니다. 이렇게 하면 권장 구성에서 참조된 데이터베이스 개체만 표에 표시됩니다. 아래 스크롤 막대를 사용하여 권장 구성 표의 가장 오른쪽 열을 보고 **정의** 열의 항목을 클릭하여 데이터베이스의 개체를 생성하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 보거나 복사합니다.  
  
6.  이 권장 구성의 모든 데이터베이스 개체를 만들거나 삭제하는 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 하나의 스크립트 파일에 저장하려면 **동작** 메뉴의 **권장 구성 저장** 을 클릭합니다.  
  
#### <a name="to-view-the-tuning-summary-and-reports-with-the-database-engine-tuning-advisor-gui"></a>데이터베이스 엔진 튜닝 관리자 GUI로 튜닝 요약 및 보고서를 보려면  
  
1.  데이터베이스 엔진 튜닝 관리자 GUI 또는 **dta** 명령줄 유틸리티를 사용하여 데이터베이스를 튜닝합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 기존 튜닝 세션을 사용하려면 이 단계를 건너뛰고 2단계를 실행합니다.  
  
2.  데이터베이스 엔진 튜닝 관리자 GUI를 시작합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 튜닝 요약 및 기존 튜닝 세션에 대한 보고서를 보려면 **세션 모니터**의 세션 이름을 두 번 클릭하여 세션을 엽니다.  
  
3.  새 튜닝 세션이 완료되거나 도구가 기존 세션을 로드한 후에 **보고서** 탭을 클릭합니다.  
  
4.  **튜닝 요약** 창에 튜닝 세션에 대해 설명합니다. **예상 향상률** 및 **권장 구성이 사용하는 공간** 항목에서 제공한 정보는 권장 구성을 구현할 것인지 여부를 결정하는 데 특히 유용할 수 있습니다.  
  
5.  **튜닝 보고서** 창에서 **보고서 선택** 을 클릭하여 보려는 튜닝 보고서를 선택합니다.  
  
#### <a name="to-view-tuning-logs-with-the-database-engine-tuning-advisor-gui"></a>데이터베이스 엔진 튜닝 관리자 GUI로 튜닝 로그를 보려면  
  
1.  데이터베이스 엔진 튜닝 관리자 GUI 또는 **dta** 명령줄 유틸리티를 사용하여 데이터베이스를 튜닝합니다. 작업을 튜닝할 때 **일반** 탭의 **튜닝 로그 저장** 을 선택했는지 확인합니다. 기존 튜닝 세션을 사용하려면 이 단계를 건너뛰고 2단계를 실행합니다.  
  
2.  데이터베이스 엔진 튜닝 관리자 GUI를 시작합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 기존 튜닝 세션에 대한 튜닝 요약 및 보고서를 보려면 **세션 모니터** 창에서 세션 이름을 두 번 클릭하여 세션을 엽니다.  
  
3.  새 튜닝 세션이 완료되거나 도구가 기존 세션을 로드한 후에 **진행률** 탭을 클릭합니다. **튜닝 로그** 창은 로그 내용을 표시합니다. 로그에는 데이터베이스 엔진 튜닝 관리자가 분석할 수 없는 작업 이벤트에 대한 정보가 있습니다.  
  
     데이터베이스 엔진 튜닝 관리자가 튜닝 세션의 모든 이벤트를 분석한 경우 세션에 대한 튜닝 로그가 비어 있다는 메시지가 표시됩니다. 처음에 튜닝 세션을 실행할 때 **일반** 탭의 **튜닝 로그 저장** 을 선택하지 않은 경우 이러한 내용을 나타내는 메시지가 표시됩니다.  
  
##  <a name="Implement"></a> 튜닝 권장 구성 구현  
 튜닝 세션 도중 수동 또는 자동으로 데이터베이스 엔진 튜닝 관리자 권장 구성을 구현할 수 있습니다. 이 권장 구성을 구현하기 전에 먼저 튜닝 결과를 확인하려면 데이터베이스 엔진 튜닝 관리자 GUI를 사용하세요. 그러면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 데이터베이스 엔진 튜닝 관리자에서 권장 구성을 구현하기 위한 작업 분석 결과로서 생성되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 수동으로 실행할 수 있습니다. 스크립트를 구현하기 전에 결과를 조사할 필요가 없는 경우 **dta** 명령 프롬프트 유틸리티에 **-a** 옵션을 사용할 수 있습니다. 이렇게 하면 유틸리티가 해당 작업을 분석한 후 튜닝 권장 사항을 자동으로 구현합니다. 다음 절차에서는 두 가지 데이터베이스 엔진 튜닝 관리자 인터페이스를 사용하여 튜닝 권장 구성을 구현하는 방법을 설명합니다.  
  
#### <a name="to-manually-implement-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>데이터베이스 엔진 튜닝 관리자 GUI를 사용하여 튜닝 권장 구성을 수동으로 구현하려면  
  
1.  데이터베이스 엔진 튜닝 관리자 GUI 또는 **dta** 명령 프롬프트 유틸리티를 사용하여 데이터베이스를 튜닝합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 기존 튜닝 세션을 사용하려면 이 단계를 건너뛰고 2단계를 실행합니다.  
  
2.  데이터베이스 엔진 튜닝 관리자 GUI를 시작합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 기존의 튜닝 세션에 대해 튜닝 권장 구성을 구현하려면 **세션 모니터**에서 세션 이름을 두 번 클릭하여 세션을 엽니다.  
  
3.  새 튜닝 세션이 완료된 후나 기존 세션이 도구에 로드된 후 **동작** 메뉴의 **권장 구성 적용** 을 클릭합니다.  
  
4.  **권장 구성 적용** 대화 상자에서 **지금 적용** 또는 **나중에 적용하도록 예약**을 선택합니다. **나중에 적용하도록 예약**을 선택할 경우 알맞은 날짜와 시간을 선택합니다.  
  
5.  **확인** 을 클릭하여 권장 구성을 적용합니다.  
  
#### <a name="to-automatically-implement-tuning-recommendations-using-the-dta-command-prompt-utility"></a>dta 명령 프롬프트 유틸리티를 사용하여 튜닝 권장 구성을 자동으로 구현하려면  
  
1.  데이터베이스 엔진 튜닝 관리자가 분석 중에 추가, 제거 또는 유지해야 할 데이터베이스 기능(인덱스, 인덱싱된 뷰, 분할)을 결정합니다.  
  
     튜닝을 시작하기 전에 다음 사항을 고려해야 합니다.  
  
    -   추적 테이블을 작업 테이블로 사용하는 경우 해당 테이블은 데이터베이스 엔진 튜닝 관리자가 튜닝 중인 서버와 동일한 서버에 있어야 합니다. 다른 서버에 추적 테이블을 만들 경우에는 데이터베이스 엔진 튜닝 관리자가 튜닝하는 서버로 이 테이블을 이동합니다.  
  
    -   튜닝 세션이 예상보다 오랫동안 계속 실행되면 Ctrl+C를 눌러 튜닝 세션을 끝낼 수 있습니다. 이 경우 Ctrl+C를 누르면 작업 튜닝에 이미 사용된 시간이 허비되지 않도록 **dta** 는 사용한 작업량에 따라 가능한 최적의 권장 구성을 강제로 생성합니다.  
  
2.  명령 프롬프트에서 다음을 입력합니다.  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName -a  
    ```  
  
     여기서 **-E** 는 로그인 ID와 암호 대신 트러스트된 연결이 튜닝 세션에 사용되도록 지정하고, **-D** 는 튜닝할 데이터베이스의 이름이나 작업에 사용되는 여러 데이터베이스의 쉼표로 구분된 목록을 지정하며, **-if** 는 작업 파일의 이름과 경로를 지정합니다. 또한 **-s** 는 튜닝 세션의 이름을 지정하고, **-a** 는 작업이 분석된 후 **dta** 명령 프롬프트 유틸리티에서 사용자에게 확인하지 않고 자동으로 튜닝 권장 구성을 적용하도록 지정합니다. **dta** 명령 프롬프트 유틸리티를 사용하여 데이터베이스를 튜닝하는 방법에 대한 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
3.  Enter 키를 누릅니다.  
  
##  <a name="Analysis"></a> 탐구 분석 수행  
 데이터베이스 관리자는 데이터베이스 엔진 튜닝 관리자의 사용자 지정 구성 기능을 통해 탐구 분석을 수행할 수 있습니다. 데이터베이스 관리자는 이 기능을 사용하여 원하는 물리적 데이터베이스 디자인을 데이터베이스 엔진 튜닝 관리자에 지정함으로써 해당 디자인을 구현하지 않고서도 성능 효과를 평가할 수 있습니다. 사용자 지정 구성은 데이터베이스 엔진 튜닝 관리자의 GUI(그래픽 사용자 인터페이스) 및 명령줄 유틸리티에서 모두 지원되지만 명령줄 유틸리티가 가장 높은 유연성을 제공합니다.  
  
 데이터베이스 엔진 튜닝 관리자 GUI를 사용하는 경우 데이터베이스 엔진 튜닝 관리자의 튜닝 권장 구성에 따른 하위 집합 구현의 효과를 평가할 수는 있지만 데이터베이스 엔진 튜닝 관리자에 대해 평가할 가상 물리적 디자인 구조를 추가할 수 없습니다.  
  
 다음 절차에서는 사용자 지정 구성 기능을 두 도구 인터페이스에서 사용하는 방법에 대해 설명합니다.  
  
### <a name="using-database-engine-tuning-advisor-gui-to-evaluate-tuning-recommendations"></a>데이터베이스 엔진 튜닝 관리자 GUI를 사용한 튜닝 권장 구성 평가  
 이 절차에서는 데이터베이스 엔진 튜닝 관리자가 생성한 권장 구성을 평가하는 방법을 설명합니다. 단, GUI에서는 평가를 위한 새 물리적 디자인 구조를 지정할 수 없습니다.  
  
##### <a name="to-evaluate-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>데이터베이스 엔진 튜닝 관리자 GUI로 튜닝 권장 구성을 평가하려면  
  
1.  데이터베이스 엔진 튜닝 관리자 GUI를 사용하여 데이터베이스를 튜닝합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 기존 튜닝 세션을 평가하려면 **세션 모니터**를 두 번 클릭합니다.  
  
2.  **권장 구성** 탭에서 사용하지 않을 권장 물리적 디자인 구조를 지웁니다.  
  
3.  **동작** 메뉴에서 **권장 구성 평가**를 클릭합니다. 새 튜닝 세션이 생성됩니다.  
  
4.  새 **세션 이름**을 입력합니다. 평가 중인 물리적 데이터베이스 디자인 구조를 보려면 데이터베이스 엔진 튜닝 관리자 응용 프로그램 창 아래쪽에 있는 **설명** 부분에서 **구성 섹션을 보려면 여기를 클릭하세요** 를 선택합니다.  
  
5.  도구 모음에서 **분석 시작** 단추를 클릭합니다. 데이터베이스 엔진 튜닝 관리자가 완료되면 **권장 구성** 탭에서 결과를 볼 수 있습니다.  
  
### <a name="using-database-engine-tuning-advisor-gui-to-export-tuning-session-results-for-what-if-tuning-analysis"></a>데이터베이스 엔진 튜닝 관리자 GUI를 사용하여 "가정(what-if)" 튜닝 분석에 대한 튜닝 세션 결과 내보내기  
 다음 절차에서는 데이터베이스 엔진 튜닝 관리자의 튜닝 세션 결과를 편집할 수 있는 XML 파일로 내보낸 다음 **dta** 명령줄 유틸리티로 튜닝하는 방법을 설명합니다. 이렇게 하면 필요한 성능 향상을 이끌어 낼 수 있는지 확인하기 위해 가상의 새 물리적 디자인 구조를 데이터베이스에 구현하는 데 따른 오버헤드를 발생시키지 않고도 튜닝 분석을 수행할 수 있습니다. 데이터베이스 엔진 튜닝 관리자 GUI로 데이터베이스를 튜닝한 다음 튜닝 결과를 **.xml** 파일로 내보내는 것은 XML에 생소한 사용자가 데이터베이스 엔진 튜닝 관리자 XML 스키마의 유연성을 사용하여 "가정(what-if)" 분석을 수행할 수 있는 유용한 방법입니다.  
  
##### <a name="to-export-tuning-session-results-from-the-database-engine-tuning-advisor-gui-for-what-if-analysis-with-the-dta-command-line-utility"></a>dta 명령줄 유틸리티로 "가정(what-if)" 분석을 하기 위해 데이터베이스 엔진 튜닝 관리자 GUI의 튜닝 세션 결과를 내보내려면  
  
1.  데이터베이스 엔진 튜닝 관리자 GUI를 사용하여 데이터베이스를 튜닝합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요. 기존 튜닝 세션을 평가하려면 **세션 모니터**를 두 번 클릭합니다.  
  
2.  **파일** 메뉴에서 **세션 결과 내보내기** 를 클릭한 다음 XML 파일로 저장합니다.  
  
3.  2단계에서 만든 XML 파일을 선호하는 XML 편집기, 텍스트 편집기 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 엽니다. **Configuration** 요소로 스크롤합니다. **Configuration** 요소 섹션을 복사하여 XML 입력 파일 템플릿의 **TuningOptions** 요소 다음에 붙여 넣습니다. XML 입력 파일을 저장합니다.  
  
4.  3단계에서 새로 만든 XML 입력 파일에서 원하는 튜닝 옵션을 **TuningOptions** 요소에 지정하고 **Configuration** 요소 섹션을 편집하고(분석에 적합하도록 물리적 디자인 구조를 추가 또는 삭제) 파일을 저장한 다음 데이터베이스 엔진 튜닝 관리자 XML 스키마에 대해 유효성을 검사합니다. 이 XML 파일을 편집하는 방법은 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)를 참조하세요.  
  
5.  4단계에서 만든 XML 파일을 **dta** 명령줄 유틸리티에 대한 입력으로 사용합니다. 이 도구에서 XML 입력 파일을 사용하는 방법은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)의 "dta 유틸리티를 사용하여 데이터베이스 튜닝" 섹션을 참조하세요.  
  
### <a name="using-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>사용자 지정 구성 기능과 dta 명령줄 유틸리티 사용  
 숙련된 XML 개발자인 경우 작업 및 물리적 데이터베이스 디자인 구조의 가상 구성(예: 인덱스, 인덱싱된 뷰 또는 분할)을 지정할 데이터베이스 엔진 튜닝 관리자 XML 입력 파일을 만들 수 있습니다. 그런 다음 **dta** 명령줄 유틸리티를 사용하여 이 가상 구성이 데이터베이스 쿼리 성능에 미치는 영향을 분석할 수 있습니다. 다음 절차에서는 이 과정을 단계별로 설명합니다.  
  
##### <a name="to-use-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>사용자 지정 구성 기능과 dta 명령줄 유틸리티를 사용하려면  
  
1.  튜닝 작업을 만듭니다. 이 태스크를 수행하는 방법은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)를 참조하세요.  
  
2.  [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)을 복사하여 XML 편집기 또는 텍스트 편집기에 붙여넣습니다. 이 예제를 사용하여 튜닝 세션용 XML 입력 파일을 만듭니다. 이 태스크를 수행하는 방법은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)의 "XML 입력 파일 만들기" 섹션을 참조하세요.  
  
3.  예제 XML 입력 파일에서 **TuningOptions** 및 **Configuration** 요소를 편집합니다. **TuningOptions** 요소에서 데이터베이스 엔진 튜닝 관리자가 튜닝 세션 중 고려할 물리적 디자인 구조를 지정합니다. **Configuration** 요소에서 데이터베이스 엔진 튜닝 관리자가 분석할 물리적 데이터베이스 디자인 구조의 가상 구성과 일치하는 물리적 디자인 구조를 지정합니다. **TuningOptions** 및 **Configuration** 부모 요소에 사용할 수 있는 특성 및 자식 요소에 대한 자세한 내용은 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)를 참조하세요.  
  
4.  입력 파일을 **.xml** 확장명으로 저장합니다.  
  
5.  데이터베이스 엔진 튜닝 관리자 XML 스키마에 대해 4단계에서 저장한 XML 입력 파일의 유효성을 검사합니다. 이 스키마는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 다음 위치에 설치됩니다.  
  
    ```  
    C:\Program Files\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
    ```  
  
     또한 데이터베이스 엔진 튜닝 관리자 XML 스키마는 [http://schemas.microsoft.com/sqlserver/2004/07/dta](http://schemas.microsoft.com/sqlserver/2004/07/dta)에서 온라인으로도 제공됩니다.  
  
6.  작업 및 XML 입력 파일을 만든 후에는 분석을 위해 **dta** 명령줄 유틸리티에 이 입력 파일을 전송할 수 있습니다. **-ox** 유틸리티 인수에 XML 출력 파일 이름을 지정했는지 확인하세요. 이렇게 하면 **Configuration** 요소에 지정된 권장 구성으로 XML 출력 파일이 생성됩니다. 이 출력에 따른 다른 가상 구성을 확인하기 위해 데이터베이스 엔진 튜닝 관리자를 다시 실행하려면 출력 파일에서 **Configuration** 요소 내용을 복사하여 원본 또는 새 XML 입력 파일에 붙여 넣습니다. **dta** 유틸리티에서 XML 입력 파일을 사용하는 방법에 대한 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)의 "dta 유틸리티를 사용하여 데이터베이스 튜닝" 섹션을 참조하세요.  
  
     튜닝을 완료한 다음 데이터베이스 엔진 튜닝 관리자 GUI를 사용하여 튜닝 보고서를 보거나 XML 출력 파일을 열어 **TuningSummary** 및 **Configuration** 요소의 데이터베이스 엔진 튜닝 관리자 권장 구성을 볼 수 있습니다. 튜닝 세션의 결과를 보는 방법은 이 항목의 앞부분에 나오는 [튜닝 출력 보기](#View) 를 참조하세요. XML 출력 파일에는 데이터베이스 엔진 튜닝 관리자 분석 보고서가 포함될 수 있습니다.  
  
7.  6단계와 7단계를 반복하여 쿼리 성능을 필요한 만큼 향상시키는 가상 구성을 만듭니다. 그런 다음 새 구성을 구현할 수 있습니다. 자세한 내용은 이 항목의 앞부분에 나오는 [튜닝 권장 구성 구현](#Implement) 을 참조하세요.  
  
##  <a name="ReviewEvaluateClone"></a> 튜닝 세션 검토, 평가 및 복제  
 데이터베이스 엔진 튜닝 관리자에서는 데이터베이스에 대한 작업 영향 분석을 시작할 때마다 새 튜닝 세션을 만듭니다. 데이터베이스 엔진 튜닝 관리자 GUI의 **세션 모니터** 를 사용하여 지정한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 실행된 모든 튜닝 세션을 보거나 다시 로드할 수 있습니다. 기존의 튜닝 세션을 모두 검토할 수 있으면 기존 세션에서 세션을 복제하거나, 기존의 튜닝 권장 구성을 편집한 다음 데이터베이스 엔진 튜닝 관리자를 사용하여 편집된 세션을 평가하거나, 정기적으로 튜닝을 수행하여 데이터베이스의 물리적 디자인을 모니터링하는 등의 작업을 쉽게 수행할 수 있습니다. 예를 들어 월별 일정으로 데이터베이스를 튜닝하도록 결정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 튜닝 세션을 검토하려면 먼저 데이터베이스 엔진 튜닝 관리자를 사용하여 작업을 튜닝하여 서버 인스턴스에 튜닝 세션을 만들어야 합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
### <a name="review-existing-tuning-sessions"></a>기존 튜닝 세션 검토  
 다음 단계를 사용하여 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 기존 튜닝 세션을 찾아봅니다.  
  
##### <a name="to-review-existing-tuning-sessions"></a>기존 튜닝 세션을 검토하려면  
  
1.  데이터베이스 엔진 튜닝 관리자 GUI를 시작합니다. 자세한 내용은 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
2.  **세션 모니터** 창의 상단에 모든 기존 튜닝 세션이 표시됩니다. 표시된 세션 수는 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스를 튜닝한 횟수에 따라 달라집니다. 스크롤 막대를 사용하여 모든 튜닝 세션을 볼 수 있습니다.  
  
3.  튜닝 세션 이름을 한 번 클릭하면 **세션 모니터** 창의 하단에 해당 세부 사항이 나타납니다.  
  
4.  튜닝 세션 이름을 두 번 클릭하면 해당 정보가 데이터베이스 엔진 튜닝 관리자로 로드됩니다. 세션 정보가 로드된 후에 탭을 선택하여 이 튜닝 세션에 대한 정보를 볼 수 있습니다.  
  
### <a name="evaluate-existing-tuning-sessions-as-hypothetical-configurations"></a>기존 튜닝 세션을 가상 구성으로 평가  
 다음 단계를 사용하여 기존 튜닝 세션을 평가할 수 있습니다. 기존 튜닝 세션 평가는 해당 권장 구성을 보고 편집한 다음 다시 튜닝하는 작업입니다. 예를 들어 **table1**에 대한 인덱스만 만들려면 기존 튜닝 권장 구성에서 만들어진 인덱싱된 뷰와 분할을 삭제합니다. 그런 다음 데이터베이스 엔진 튜닝 관리자는 새 튜닝 세션을 만들고 편집된 권장 구성을 가상 구성으로 사용하여 데이터베이스에 대한 작업을 튜닝합니다. 이렇게 하면 데이터베이스 엔진 튜닝 관리자가 편집된 권장 구성이 구현된 것처럼 데이터베이스에 대한 작업을 튜닝하므로 제한된 "가정(what-if)" 분석을 수행할 수 있습니다. 데이터베이스 엔진 튜닝 관리자 GUI를 사용할 경우에는 기존 권장 구성의 하위 집합만 선택할 수 있으므로 제한된 가정 분석을 수행하게 됩니다. 이전 튜닝 세션의 하위 집합이 아닌 완전히 새로운 가상 구성을 지정하는 전체 가상 분석을 수행하려면 데이터베이스 엔진 튜닝 관리자 XML 입력 파일에 **dta** 명령줄 유틸리티를 사용해야 합니다.  
  
##### <a name="to-evaluate-an-existing-tuning-session"></a>기존 튜닝 세션을 평가하려면  
  
1.  데이터베이스 엔진 튜닝 관리자를 시작한 다음 **세션 모니터**의 상단에 있는 튜닝 세션을 두 번 클릭하면 세션 정보가 데이터베이스 엔진 튜닝 관리자에 로드됩니다.  
  
2.  **진행률** 탭을 클릭하여 데이터베이스 엔진 튜닝 관리자에서 튜닝할 수 없는 작업의 모든 이벤트에 대한 오류 정보가 들어 있는 튜닝 로그를 확인할 수 있습니다. 이 정보를 사용하면 작업의 효율성을 평가할 수 있습니다.  
  
3.  이 세션의 자세한 튜닝 결과를 검토하려면 **보고서** 탭을 클릭합니다. 여기서 튜닝 요약을 보거나 **보고서 선택** 목록에서 튜닝 보고서를 선택할 수 있습니다.  
  
4.  **권장 구성** 탭을 클릭하여 튜닝 권장 구성을 봅니다.  
  
5.  구현 여부에 대한 확신이 없는 권장 구성이 있으면 해당 권장 구성의 선택을 취소합니다.  
  
6.  **동작** 메뉴에서 **권장 구성 평가**를 클릭합니다. 데이터베이스 엔진 튜닝 관리자는 편집된 권장 구성을 가상 구성으로 사용할 새 튜닝 세션을 만듭니다. 가상 구성을 XML로 보려면 **구성 섹션을 보려면 여기를 클릭하세요**를 선택합니다.  
  
7.  **일반** 탭에서 **세션 이름**을 입력하고 올바른 **작업** 이 지정되었는지 확인합니다.  
  
8.  **튜닝 옵션** 탭에서 튜닝 시간을 지정하거나 **고급 옵션**을 지정할 수 있습니다.  
  
9. 도구 모음에서 **분석 시작** 단추를 클릭합니다. 데이터베이스 엔진 튜닝 관리자는 가상 구성을 사용하여 데이터베이스 튜닝을 시작합니다. 데이터베이스 엔진 튜닝 관리자가 완료되면 다른 세션과 동일한 방법으로 이 세션의 결과를 확인할 수 있습니다.  
  
### <a name="clone-existing-tuning-sessions"></a>기존 튜닝 세션 복제  
 데이터베이스 엔진 튜닝 관리자에서 복제 옵션을 선택하여 기존 세션을 기반으로 새 튜닝 세션을 만들 수 있습니다. 복제 옵션을 선택하면 새 튜닝 세션은 기존 세션을 기반으로 만들어집니다. 그런 다음 필요에 따라 새 세션의 튜닝 옵션을 변경할 수 있습니다. 이전 절차에서 설명한 대로 기존 세션을 평가할 때 데이터베이스 엔진 튜닝 관리자는 새 튜닝 세션도 만들지만 튜닝 옵션은 변경할 수 없습니다.  
  
##### <a name="to-create-new-tuning-sessions-by-cloning-existing-sessions"></a>기존 세션을 복제하여 새 튜닝 세션을 만들려면  
  
1.  데이터베이스 엔진 튜닝 관리자를 시작한 다음 **세션 모니터**의 상단에 있는 튜닝 세션을 두 번 클릭하면 세션 정보가 데이터베이스 엔진 튜닝 관리자에 로드됩니다.  
  
2.  **동작** 메뉴에서 **세션 복제**를 클릭합니다.  
  
3.  **일반** 탭에서 **세션 이름**을 입력하고 올바른 **작업** 이 지정되었는지 확인합니다.  
  
4.  **튜닝 옵션** 탭에서 튜닝 시간, 데이터베이스 엔진 튜닝 관리자에서 작성해야 할 물리적 디자인 구조 및 권장 구성에서 삭제해야 할 항목을 지정할 수 있습니다.  
  
5.  권장 구성에 필요한 공간 제한, 인덱스당 최대 열 개수 및 데이터베이스 엔진 튜닝 관리자에서 **가 온라인 상태일 때 구현할 수 있는 권장 구성을 생성할지 여부를 설정하려면** 고급 옵션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 클릭합니다.  
  
6.  도구 모음에서 **분석 시작** 단추를 클릭하여 다른 튜닝 세션처럼 작업의 영향을 분석할 수 있습니다. 데이터베이스 엔진 튜닝 관리자가 완료되면 다른 세션과 동일한 방법으로 이 세션의 결과를 확인할 수 있습니다.  
  
##  <a name="UI"></a> 사용자 인터페이스 설명  
  
### <a name="sessions-monitor"></a>세션 모니터  
 **세션 모니터** 는 데이터베이스 엔진 튜닝 관리자에서 연 세션에 대한 정보를 표시합니다. 세션 정보를 속성 창에 표시하려면 **세션 모니터**에서 세션 이름을 선택합니다.  
  
### <a name="recommendations-tab"></a>권장 구성 탭  
 **권장 구성** 탭은 데이터베이스 엔진 튜닝 관리자가 작업 분석을 완료한 후 표시됩니다. 이 표에는 고려 대상인 각 개체에 대한 권장 구성이 포함되어 있습니다. 파티션 권장 구성은 위쪽 표에 표시되고 인덱스 권장 구성은 아래쪽 표에 표시됩니다. 권장 구성이 없으면 표가 표시되지 않습니다.  
  
 **정의** 열에는 권장 파티션 또는 인덱스에 대한 정의가 하이퍼링크로 표시됩니다. 대개 이 열은 좁아서 전체 정의를 볼 수 없습니다. 전체 정의 및 **클립보드로 복사** 단추가 있는 대화 상자를 표시하려면 하이퍼링크를 클릭합니다.  
  
#### <a name="partition-recommendations"></a>파티션 권장 구성  
 **데이터베이스 이름**  
 수정하도록 권장되는 개체가 포함된 데이터베이스입니다.  
  
 **권장**  
 성능 향상을 위해 권장되는 동작입니다. 사용할 수 있는 값은 만들기 및 삭제입니다.  
  
 **권장 구성의 대상**  
 권장 구성의 영향을 받는 파티션 함수 또는 구성표입니다. 이 열의 아이콘은 권장되는 사항이 **권장 구성의 대상** 에 대한 삭제인지 아니면 추가인지 여부와, 대상이 파티션 함수인지 또는 구성표인지를 나타냅니다.  
  
 **세부 정보**  
 **권장 구성의 대상**에 대한 설명입니다. 사용할 수 있는 값은 파티션 함수의 경우 범위이고 파티션 구성표의 경우 공백입니다.  
  
 **파티션 수**  
 권장 파티션 함수가 정의하는 파티션 수입니다. 이 함수를 구성표와 함께 사용한 후 테이블에 적용하면 테이블 데이터가 해당 파티션 수로 나뉩니다.  
  
 **정의**  
 **권장 구성의 대상**에 대한 정의입니다. 권장되는 동작에 대한 스크립트와 함께 SQL 스크립트 미리 보기 대화 상자를 열려면 해당 열을 클릭합니다.  
  
##### <a name="index-recommendations"></a>인덱스 권장 구성  
 **데이터베이스 이름**  
 수정하도록 권장되는 개체가 포함된 데이터베이스입니다.  
  
 **Object Name**  
 권장 구성과 관련된 테이블입니다.  
  
 **권장**  
 성능 향상을 위해 권장되는 동작입니다. 사용할 수 있는 값은 만들기 및 삭제입니다.  
  
 **권장 구성의 대상**  
 권장 구성의 영향을 받는 인덱스 또는 뷰입니다. 이 열의 아이콘은 권장되는 사항이 **권장 구성의 대상**에 대한 삭제인지 아니면 추가인지 여부를 나타냅니다.  
  
 **세부 정보**  
 **권장 구성의 대상**에 대한 설명입니다. 사용될 수 있는 값은 클러스터형, 인덱싱된 뷰 또는 비클러스터형 인덱스를 나타내는 공백입니다. 인덱스가 고유한지 여부도 나타냅니다.  
  
 **파티션 구성표**  
 파티션이 권장되는 경우 이 열에 파티션 구성표가 제공됩니다.  
  
 **크기(KB)**  
 권장되는 새 개체의 예상 크기입니다. 이 열이 비어 있으면 **기존 개체의 크기에 대한 보고서를 참조하세요**를 클릭합니다.  
  
 **정의**  
 **권장 구성의 대상**에 대한 정의입니다. 권장되는 동작에 대한 스크립트와 함께 SQL 스크립트 미리 보기 대화 상자를 열려면 해당 열을 클릭합니다.  
  
 **권장 구성**  
 데이터베이스 엔진 튜닝 관리자에서 만든 개체에 대한 권장 구성에 포함되지 않은 기존 개체도 모두 표에 표시하려면 선택합니다.  
  
 **기존 개체의 크기에 대한 보고서를 참조하세요**  
 기존 개체의 크기를 권장 구성 표에 제공하는 보고서를 보려면 선택합니다.  
  
### <a name="actions-menuapply-recommendations-options"></a>동작 메뉴/권장 구성 적용 옵션  
 작업 분석이 완료되고 권장 구성이 제시되면 **동작** 메뉴에서 **권장 구성 적용** 을 클릭하여 **권장 구성 적용** 대화 상자를 엽니다.  
  
 **지금 적용**  
 권장 구성에 대한 스크립트를 생성하고 스크립트를 실행하여 권장 구성을 구현합니다.  
  
 **나중에 적용하도록 예약**  
 권장 구성에 대한 스크립트를 생성하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업으로 동작을 저장합니다.  
  
 **날짜**  
 권장 구성을 적용하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 실행할 날짜를 지정합니다.  
  
 **Time**  
 권장 구성을 적용하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 실행할 시간을 지정합니다.  
  
### <a name="reports-tab-options"></a>보고서 탭 옵션  
 **보고서** 탭은 데이터베이스 엔진 튜닝 관리자가 작업 분석을 완료한 후 표시됩니다.  
  
 **튜닝 요약**  
 데이터베이스 엔진 튜닝 관리자의 권장 구성을 요약하여 표시합니다.  
  
 **날짜**  
 데이터베이스 엔진 튜닝 관리자가 보고서를 만든 날짜입니다.  
  
 **Time**  
 데이터베이스 엔진 튜닝 관리자가 보고서를 만든 시간입니다.  
  
 **Server**  
 데이터베이스 엔진 튜닝 관리자 작업의 대상이 되는 서버입니다.  
  
 **튜닝할 데이터베이스**  
 데이터베이스 엔진 튜닝 관리자의 권장 구성이 적용되는 데이터베이스입니다.  
  
 **작업 파일**  
 작업이 파일인 경우 나타납니다.  
  
 **작업 테이블**  
 작업이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블인 경우 나타납니다.  
  
 **작업**  
 작업을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 편집기에서 가져온 경우 나타납니다.  
  
 **최대 튜닝 시간**  
 데이터베이스 엔진 튜닝 관리자 분석에 사용할 수 있도록 구성된 최대 시간입니다.  
  
 **튜닝 소요 시간**  
 데이터베이스 엔진 튜닝 관리자가 작업을 분석하는 데 실제로 사용한 시간입니다.  
  
 **예상 향상률**  
 데이터베이스 엔진 튜닝 관리자의 모든 권장 구성이 적용된 경우 대상 작업의 예상 향상률입니다.  
  
 **권장 구성에 필요한 최대 공간(MB)**  
 권장 구성에 필요한 최대 공간입니다. 이 값은 분석을 시작하기 전에 **튜닝 옵션** 탭의 **고급 옵션** 단추를 사용하여 구성합니다.  
  
 **현재 사용 중인 공간(MB)**  
 분석 중인 데이터베이스의 인덱스가 현재 사용하는 공간입니다.  
  
 **권장 구성이 사용하는 공간(MB)**  
 데이터베이스 엔진 튜닝 관리자의 모든 권장 구성이 적용된 경우 인덱스가 사용할 것으로 예상되는 공간입니다.  
  
 **작업 이벤트 수**  
 작업에 포함된 이벤트 수입니다.  
  
 **튜닝된 이벤트 수**  
 작업의 튜닝된 이벤트 수입니다. 이벤트를 튜닝할 수 없는 경우 **진행률** 탭의 튜닝 로그에 표시됩니다.  
  
 **튜닝된 문 수**  
 작업의 튜닝된 문 수입니다. 문을 튜닝할 수 없는 경우 **진행률** 탭의 튜닝 로그에 표시됩니다.  
  
 **튜닝된 집합에서의 SELECT 문 비율**  
 튜닝된 문 중 SELECT 문의 비율입니다. 튜닝된 SELECT 문이 있을 경우에만 나타납니다.  
  
 **튜닝된 집합에서의 UPDATE 문 비율**  
 튜닝된 문 중 UPDATE 문의 비율입니다. 튜닝된 UPDATE 문이 있을 경우에만 나타납니다.  
  
 **권장되는 인덱스 생성(또는 삭제) 수**  
 튜닝된 데이터베이스에서 생성 또는 삭제하도록 권장되는 인덱스 수입니다. 인덱스가 권장 구성에 포함된 경우에만 나타납니다.  
  
 **뷰에서 권장되는 인덱스 생성(또는 삭제) 수**  
 튜닝된 데이터베이스의 뷰에서 생성 또는 삭제하도록 권장되는 인덱스 수입니다. 뷰의 인덱스가 권장 구성에 포함된 경우에만 나타납니다.  
  
 **권장되는 통계 생성 수**  
 튜닝된 데이터베이스에서 생성하도록 권장되는 통계 수입니다. 통계가 권장되는 경우에만 나타납니다.  
  
 **Select Report**  
 선택한 보고서에 대한 자세한 정보를 볼 수 있습니다. 표의 열은 보고서마다 다릅니다.  
  
## <a name="see-also"></a>참고 항목  
 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [dta 유틸리티](../../tools/dta/dta-utility.md)  
  
  

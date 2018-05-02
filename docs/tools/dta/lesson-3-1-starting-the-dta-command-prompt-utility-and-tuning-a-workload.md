---
title: dta 명령 프롬프트 유틸리티 시작 및 작업 튜닝 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: f34a5acf-1f3b-4484-a770-6470cb925ab0
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4adf756444c22146108fead4f607c20c6108dc3
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-3-1---starting-the-dta-command-prompt-utility-and-tuning-a-workload"></a>3-1단원 - dta 명령 프롬프트 유틸리티 시작 및 작업 튜닝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 태스크에서는 **dta** 유틸리티를 시작하고 도움말을 본 다음, 이 유틸리티를 사용하여 명령 프롬프트에서 작업을 튜닝하는 과정을 안내합니다. 여기서는 데이터베이스 엔진 튜닝 관리자 GUI(그래픽 사용자 인터페이스) 연습인 [작업 튜닝](../../tools/dta/lesson-1-1-tuning-a-workload.md)에 대해 만든 MyScript.sql 작업을 사용합니다.  
  
이 자습서에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 사용합니다. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. 예제 데이터베이스를 설치하려면 [SQL Server 예제 및 예제 데이터베이스](http://sqlserversamples.codeplex.com)를 참조하세요.  
  
다음 태스크에서는 명령 프롬프트를 열고 **dta** 명령 프롬프트 유틸리티를 시작하고 구문 도움말을 본 다음 [Tuning a Workload](../../tools/dta/lesson-1-1-tuning-a-workload.md)에서 만든 단순 작업인 MyScript.sql을 튜닝하는 과정을 안내합니다.  
  
### <a name="to-start-the-dta-command-prompt-utility-and-view-help"></a>dta 명령 프롬프트 유틸리티를 시작하고 도움말을 보려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **보조프로그램**을 차례로 가리킨 다음 **명령 프롬프트**를 클릭합니다.  
  
2.  명령 프롬프트에 다음을 입력하고 Enter 키를 누릅니다.  
  
    ```  
    dta -? | more  
    ```  
  
    이 명령의 `| more` 부분은 옵션입니다. 그러나 이 부분을 사용하여 유틸리티의 구문 도움말이 표시되는 방식을 지정할 수 있습니다. 도움말 텍스트를 한 줄씩 표시하려면 Enter 키를, 한 페이지씩 표시하려면 스페이스바를 누릅니다.  
  
### <a name="to-tune-a-simple-workload-by-using-the-dta-command-prompt-utility"></a>dta 명령 프롬프트 유틸리티를 사용하여 단순 작업을 튜닝하려면  
  
1.  명령 프롬프트에서 MyScript.sql 파일을 저장한 디렉터리로 이동합니다.  
  
2.  명령 프롬프트에 다음을 입력하고 Enter 키를 눌러 명령을 실행하고 튜닝 세션을 시작합니다. 유틸리티에서 명령 구문을 분석할 때는 대/소문자가 구분됩니다.  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
    여기서 `-S` 는 사용 중인 서버 이름과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 설치된 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 인스턴스를 지정합니다. `-E` 설정은 인스턴스에 대해 트러스트된 연결을 사용하도록 지정하는데 이는 Windows 도메인 계정으로 연결할 경우에 적합합니다. `-D` 설정은 튜닝하려는 데이터베이스를, `-if` 설정은 작업 파일을, `-s` 설정은 세션 이름을, `-of` 설정은 도구에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 권장 구성 스크립트를 작성하려는 파일을, `-ox` 설정은 도구에서 권장 구성을 XML 형식으로 작성하려는 파일을 지정합니다. 마지막 스위치 세 개는 튜닝 옵션을 지정합니다. 즉, `-fa IDX_IV` 는 데이터베이스 엔진 튜닝 관리자가 인덱스(클러스터형과 비클러스터형 모두)와 인덱싱된 뷰만 추가할 것을 고려하도록 지정하고 `-fp NONE` 은 분석하는 동안 어떠한 분할 전략도 고려하지 않도록 지정하며 `-fk NONE` 은 데이터베이스 엔진 튜닝 관리자가 해당 권장 구성을 만들 때 데이터베이스의 어떠한 기존 물리적 디자인 구조도 유지되지 않도록 지정합니다.  
  
3.  데이터베이스 엔진 튜닝 관리자에서 작업 튜닝을 마치면 튜닝 세션이 완료되었다는 메시지가 표시됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 로 MySession2OutputScript.sql 및 MySession2Output.xml 파일을 열어서 튜닝 결과를 볼 수 있습니다. 또는 [Viewing Tuning Recommendations](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md) 및 [Viewing Tuning Reports](../../tools/dta/lesson-1-3-viewing-tuning-reports.md)에서와 같은 방법으로 데이터베이스 엔진 튜닝 관리자 GUI에서 MySession2 튜닝 세션을 열고 해당 권장 구성과 보고서를 볼 수도 있습니다.  
  
## <a name="summary"></a>요약  
**dta** 유틸리티를 사용하여 명령 프롬프트에서 단순 작업 튜닝을 완료했습니다. 이 도구는 다른 많은 튜닝 옵션을 제공합니다. 자세한 내용은 도구 도움말(**dta -?**)과 참조 항목 [dta 유틸리티](../../tools/dta/dta-utility.md) 를 참조하세요.  
  
## <a name="after-you-finish-this-tutorial"></a>이 자습서를 마친 후  
이 자습서의 학습을 마친 후에는 다음 항목을 참조하여 데이터베이스 엔진 튜닝 관리자에 대한 자세한 내용을 보십시오.  
  
-   [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) - 이 도구로 태스크를 수행하는 방법에 대한 설명  
  
-   [dta Utility](../../tools/dta/dta-utility.md) - 유틸리티 작업을 제어하는 데 사용할 수 있는 명령 프롬프트 유틸리티 및 선택적 XML 파일에 대한 참조 자료  
  
자습서의 시작 부분으로 돌아가려면 [Tutorial: Database Engine Tuning Advisor](../../tools/dta/tutorial-database-engine-tuning-advisor.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 엔진 자습서](../../relational-databases/database-engine-tutorials.md)  
  
  
  

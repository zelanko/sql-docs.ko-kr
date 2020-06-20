---
title: 데이터베이스 엔진 쿼리 편집기
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: rothja
ms.author: jroth
ms.openlocfilehash: d6e70da414127936fa87ad5b410620f266a15a70
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056834"
---
# <a name="database-engine-query-editor-sql-server-management-studio"></a>데이터베이스 엔진 쿼리 편집기(SQL Server Management Studio)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 포함하는 스크립트를 만들고 실행할 수 있습니다. 또한 편집기는 **sqlcmd** 명령을 포함하는 스크립트 실행을 지원합니다.  
  
## <a name="transact-sql-f1-help"></a>Transact-SQL F1 도움말  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기는 F1 키를 선택할 때 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 대한 참조 항목을 연결할 수 있습니다. 이렇게 하려면 Transact-SQL 문의 이름을 강조 표시하고 F1 키를 선택합니다. 그러면 도움말 검색 엔진에서 강조 표시된 문자열과 일치하는 F1 도움말 특성을 가진 항목을 검색합니다.  
  
 도움말 검색 엔진에서 강조 표시된 문자열과 정확히 일치하는 F1 도움말 키워드를 포함하는 항목을 찾을 수 없을 경우 이 항목이 표시됩니다. 이 경우 다음과 같은 두 가지 방법으로 원하는 도움말을 찾을 수 있습니다.  
  
-   편집기에서 선택한 문자열을 복사한 다음 SQL Server 온라인 설명서의 검색 탭에 붙여 넣고 검색을 수행합니다.  
  
-   항목에 적용되는 F 도움말 키워드와 일치할 것으로 예상되는 Transact-SQL 문 부분만 선택한 다음 F1 키를 다시 누릅니다. 그러면 검색 엔진에서 강조 표시된 문자열과 항목에 할당된 F1 도움말 키워드를 정확하게 일치시킵니다. 강조 표시된 문자열에 열이나 매개 변수 이름과 같이 사용자 환경 고유의 요소가 포함되어 있을 경우 검색 엔진에서 일치하는 항목을 찾을 수 없습니다. 선택할 수 있는 문자열의 예는 다음과 같습니다.  
  
    -   SELECT, CREATE DATABASE, BEGIN TRANSACTION 등의 Transact-SQL 문 이름  
  
    -   SERVERPROPERTY, @@VERSION 등의 기본 제공 함수 이름  
  
    -   sys.data_spaces, sp_tableoption 등의 시스템 저장 프로시저 테이블 또는 뷰 이름  
  
## <a name="working-with-the-database-engine-query-editor"></a>데이터베이스 엔진 쿼리 편집기 작업  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 구현되는 네 가지 편집기 중 하나입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 구현되는 기능과 이 편집기를 사용하여 수행할 수 있는 주요 태스크에 대한 자세한 내용은 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../scripting/query-and-text-editors-sql-server-management-studio.md)를 참조하세요.  
  
## <a name="sql-editor-toolbar"></a>SQL 편집기 도구 모음  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기가 열려 있으면 다음 단추를 포함하는 SQL 편집기 도구 모음이 표시됩니다.  
  
 **연결**  
 **서버에 연결** 대화 상자를 엽니다. 이 대화 상자를 사용하여 서버에 연결합니다.  
  
 **케이블**  
 현재 쿼리 편집기와 서버 간의 연결을 끊습니다.  
  
 **연결 변경**  
 **서버에 연결** 대화 상자를 엽니다. 이 대화 상자를 사용하여 다른 서버에 연결합니다.  
  
 **현재 연결에서의 새 쿼리**  
 새 쿼리 편집기 창을 열고 현재 쿼리 편집기 창의 연결 정보를 사용합니다.  
  
 **사용 가능한 데이터베이스**  
 같은 서버의 다른 데이터베이스로 연결을 변경합니다.  
  
 **실행할**  
 선택한 코드를 실행하거나, 코드를 선택하지 않은 경우 쿼리 편집기에 있는 모든 코드를 실행합니다.  
  
 **디버그**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 사용합니다. 이 디버거에서는 중단점 설정, 변수 조사 및 단계별 코드 실행과 같은 디버깅 동작을 지원합니다.  
  
 **쿼리 실행 취소**  
 취소 요청을 서버로 보냅니다. 일부 쿼리는 바로 취소할 수 없으며 적절한 취소 조건이 될 때까지 기다려야 합니다. 트랜잭션을 취소해도 트랜잭션이 롤백되는 동안 작업이 지연될 수 있습니다.  
  
 **구문 분석**  
 선택한 코드의 구문을 확인합니다. 코드를 선택하지 않은 경우 쿼리 편집기 창에 있는 모든 코드의 구문을 확인합니다.  
  
 **예상 실행 계획 표시**  
 쿼리를 실제로 실행하지 않고 쿼리 프로세서에서 쿼리 실행 계획을 요청한 다음 **실행 계획** 창에 계획을 표시합니다. 이 계획은 각 쿼리 부분을 실행하는 중 반환될 것으로 예상되는 행 수의 예측으로 인덱스 통계를 사용합니다. 실제 사용되는 쿼리 계획은 예상 실행 계획과 다를 수 있습니다. 이러한 차이는 반환되는 행 수가 예상치와 크게 다를 경우에 발생할 수 있으며, 쿼리 프로세서는 쿼리 계획을 더 효율적으로 변경합니다.  
  
 **쿼리 옵션**  
 **쿼리 옵션** 대화 상자를 엽니다. 이 대화 상자를 사용하여 쿼리 실행 및 쿼리 결과에 대한 기본 옵션을 구성합니다.  
  
 **IntelliSense 사용**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 IntelliSense 기능을 사용할지를 지정합니다.  
  
 **실제 실행 계획 포함**  
 쿼리를 실행한 후 쿼리 결과와 쿼리에 사용된 실행 계획을 반환합니다. 이러한 결과는 **실행 계획** 창에 그래픽 쿼리 계획으로 표시됩니다.  
  
 **클라이언트 통계 포함**  
 쿼리 통계와 네트워크 패킷 통계 및 쿼리 경과 시간이 표시된 **클라이언트 통계** 창을 포함합니다.  
  
 **텍스트로 결과 표시**  
 쿼리 결과를 텍스트로 **결과** 창에 반환합니다.  
  
 **표 형태로 결과 표시**  
 쿼리 결과를 하나 이상의 표로 **결과** 창에 반환합니다.  
  
 **파일로 결과 저장**  
 쿼리를 실행하면 **결과 저장** 대화 상자가 열립니다. **저장 위치**에서 파일을 저장할 폴더를 선택합니다. **파일 이름**에 파일 이름을 입력하고 **저장** 을 클릭하여 쿼리 결과를 확장명이 .rpt인 **보고서** 파일로 저장합니다. 고급 옵션을 보려면 **저장** 단추의 아래쪽 화살표를 클릭한 다음 **인코딩하여 저장**을 클릭합니다.  
  
 **선택 영역을 주석으로 처리**  
 줄의 시작 부분에 주석 기호(--)를 추가하여 현재 줄을 주석으로 처리합니다.  
  
 **선택 영역의 주석 처리 제거**  
 줄의 시작 부분에서 주석 기호(--)를 제거하여 현재 줄을 활성 소스 코드 문으로 처리합니다.  
  
 **줄 내어쓰기**  
 줄의 시작 부분에서 공백을 제거하여 해당 줄의 텍스트를 왼쪽으로 이동합니다.  
  
 **줄 들여쓰기**  
 줄의 시작 부분에 공백을 추가하여 해당 줄의 텍스트를 오른쪽으로 이동합니다.  
  
 **템플릿 매개 변수 값 지정**  
 저장 프로시저 및 함수의 매개 변수 값을 지정하는 데 사용할 수 있는 대화 상자를 엽니다.  
  
 **보기** 메뉴를 선택하고 **도구 모음**을 선택한 다음 **SQL 편집기**를 선택하여 SQL 편집기 도구 모음을 추가할 수도 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창이 열려 있지 않을 때 SQL 편집기 도구 모음을 추가하면 일부 단추를 사용하지 못할 수 있습니다.  
  
## <a name="sql-editor-toolbar"></a>SQL 편집기 도구 모음  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창을 열면 **보기** 메뉴, **도구 모음**, **디버그**를 차례로 선택하여 디버그 도구 모음을 추가할 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창이 열려 있지 않을 때 디버그 도구 모음을 추가하면 일부 단추를 사용하지 못할 수 있습니다.  
  
 **계속**  
 중단점이 나올 때까지 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에서 코드를 실행합니다.  
  
 **모두 중단**  
 중단이 발생하면 디버거에 연결된 모든 프로세스를 중단하도록 디버거를 설정합니다.  
  
 **디버깅 중지**  
 선택한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에서 디버그 모드를 종료하고 표준 실행 모드로 복원합니다.  
  
 **다음 문 표시**  
 커서를 실행할 다음 문으로 이동합니다.  
  
 **한 단계씩 코드 실행**  
 다음 문이 실행됩니다. 문에서 Transact-SQL 저장 프로시저, 함수 또는 트리거를 호출하면 디버거에서 모듈 코드가 포함된 새 **쿼리 편집기** 창을 표시합니다. 창이 디버그 모드에 있으며 모듈의 첫 번째 문에서 실행이 일시 중지됩니다. 그리고 나서 중단점을 설정하거나 코드를 단계별로 실행하여 모듈을 이동할 수 있습니다.  
  
 **프로시저 단위 실행**  
 다음 문이 실행됩니다. 문에서 Transact-SQL 저장 프로시저, 함수 또는 트리거를 호출하면 모듈이 완료될 때까지 실행되고 결과가 호출 코드에 반환됩니다. 모듈에 오류가 없으면 모듈을 프로시저 단위로 실행할 수 있습니다. 이 경우 모듈 호출 이후의 문에서 실행이 일시 중지됩니다.  
  
 **프로시저 나가기**  
 다음으로 가장 높은 호출 수준(함수, 저장 프로시저 또는 트리거)으로 돌아갑니다. 저장 프로시저, 함수 또는 트리거를 호출한 후 문에서 실행이 일시 중지됩니다.  
  
 **Windows**  
 **중단점** 창 또는 **직접 실행** 창을 엽니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Management Studio 바로 가기 키](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
  
  

---
title: SQL Server 데이터베이스 단위 테스트용 테스트 프로젝트 만들기
description: SQL Server 데이터베이스 단위 테스트용 테스트 프로젝트를 만드는 방법을 알아봅니다. 데이터베이스 프로젝트를 포함하는 솔루션에 테스트 프로젝트를 추가하는 다양한 방법을 살펴봅니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 4b3e7ba8-b565-4689-af1a-34cc255b7c60
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: b5a10fdbc94858a9fe3f5b523fdd43b505e2563f
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987559"
---
# <a name="how-to-create-a-test-project-for-sql-server-database-unit-testing"></a>방법: SQL Server 데이터베이스 단위 테스트용 테스트 프로젝트 만들기

데이터베이스 개체를 평가하는 단위 테스트를 작성하려면 먼저 테스트 프로젝트를 만들어야 합니다. 이 프로젝트에는 SQL Server 단위 테스트가 포함되지만 다른 유형의 테스트도 포함될 수 있습니다.  
  
지정된 데이터베이스 프로젝트에 대한 모든 SQL Server 단위 테스트를 단일 테스트 프로젝트 내에 둘 수 있습니다. 하지만 다음 질문의 답변에 따라 추가 테스트 프로젝트를 만들 수도 있습니다.  
  
|질문|의사 결정|  
|-|-|   
|테스트 실행 또는 테스트 유효성 검사를 위해 서로 다른 SQL Server 단위 테스트로 서로 다른 데이터베이스 연결에 액세스해야 합니까?|예인 경우, 두 개 이상의 테스트 프로젝트가 필요합니다. 테스트 실행에 대해서는 두 개 이상의 데이터베이스 연결을 지정할 수 없습니다. 하지만 테스트 유효성 검사를 위해서는 다른 데이터베이스 연결을 지정할 수 있습니다.|  
|서로 다른 단위 테스트에 대해 서로 다른 데이터베이스 프로젝트를 배포해야 합니까?|예인 경우, 두 개 이상의 테스트 프로젝트가 필요합니다. 테스트 프로젝트에서는 데이터베이스 프로젝트를 하나만 배포할 수 있습니다.|  
  
이러한 각 질문에 대한 자세한 내용은 [방법: SQL Server 단위 테스트 실행 구성](../ssdt/how-to-configure-sql-server-unit-test-execution.md)을 참조하세요. 여러 테스트 프로젝트를 만드는 방법에 대한 대안으로 사용자 고유의 [DatabaseTestService](/previous-versions/visualstudio/visual-studio-2010/dd154755(v=vs.100)) Microsoft.Data.Schema.UnitTesting.DatabaseTestService 구현을 제공할 수도 있습니다.  
  
데이터베이스 프로젝트가 포함된 솔루션에 테스트 프로젝트를 추가하는 데는 세 가지 옵션을 사용할 수 있습니다.  
  
-   솔루션에 테스트 프로젝트를 추가합니다. 테스트 프로젝트에는 표준 단위 테스트(삭제 가능)가 포함됩니다. 이 프로젝트에는 사용자가 추가해야 하는 SQL Server 단위 테스트 클래스가 포함되지 않습니다.  
  
-   **테스트** 메뉴에서 새 SQL Server 단위 테스트를 추가합니다. 단위 테스트를 추가하면 SQL Server Data Tools에서 테스트 프로젝트도 만듭니다(요청한 경우). 이 프로젝트에는 SQL Server 단위 테스트 클래스가 포함되어 있습니다. SQL Server 단위 테스트 클래스에는 하나 이상의 SQL Server 단위 테스트가 포함되어 있습니다.  
  
-   SQL Server 개체 탐색기에 열려 있는 프로젝트에서 저장 프로시저, 함수 또는 트리거를 토대로 단위 테스트를 만듭니다. 단위 테스트를 만들면 SQL Server Data Tools에서 테스트 프로젝트도 만듭니다(요청한 경우). 이 프로젝트에는 SQL Server 단위 테스트 클래스가 포함되어 있습니다. SQL Server 테스트 클래스에는 하나 이상의 단위 테스트가 포함되어 있습니다.  
  
다음 절차에서는 각 접근 방법에 대해 설명합니다.  
  
### <a name="to-add-a-test-project-to-an-existing-solution"></a>기존 솔루션에 기존 테스트 프로젝트를 추가하려면  
  
1.  **파일** 메뉴에서 **새로 만들기**를 가리키고 **프로젝트**를 클릭합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
2.  **설치된 템플릿**에서 **SQL Server** 노드를 확장한 후 **SQL Server 데이터베이스 프로젝트**를 선택합니다.  
  
3.  **이름**에 프로젝트 이름을 입력합니다.  
  
### <a name="to-create-a-test-project-with-a-sql-server-unit-test-class"></a>SQL Server 단위 테스트 클래스로 테스트 프로젝트를 만들려면  
  
-   [방법: 빈 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-an-empty-sql-server-unit-test.md) 또는 [방법: 함수, 트리거 및 저장 프로시저에 대한 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)에 설명된 절차를 따릅니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  

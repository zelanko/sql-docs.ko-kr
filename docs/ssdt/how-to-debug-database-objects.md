---
title: 데이터베이스 개체 디버그
description: 저장 프로시저, 함수 및 트리거를 디버그하는 방법을 알아봅니다. 디버깅을 켜고, 중단점을 설정하고, 디버그 모드에서 SQL Server 단위 테스트를 실행하는 방법을 확인합니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: f5d4584f-e85f-4558-b056-83681c365978
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 9a9e1b3b6dd7e46872c6196ef3257805c1f5a72f
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2020
ms.locfileid: "85518763"
---
# <a name="how-to--debug-database-objects"></a>방법:  데이터베이스 개체 디버그

SQL Server 단위 테스트는 다음 항목으로 구성됩니다.  
  
-   Visual C\# 또는 Visual Basic으로 작성된 단위 테스트 코드. SQL Server 단위 테스트 디자이너에서 생성되는 이 코드는 테스트 본문을 구성하는 Transact\-SQL 스크립트를 전송하는 역할을 합니다.  
  
-   Visual C\# 또는 Visual Basic으로 작성된 하나 이상의 테스트 조건. 테스트 조건을 디버그하려면 [방법: 테스트 실행 도중 디버그(Visual Studio 2010)](https://msdn.microsoft.com/library/ms182484(VS.100).aspx) 또는 [방법: 테스트 실행 도중 디버그(Visual Studio 2012)](https://msdn.microsoft.com/library/ms182484.aspx)에 설명된 단위 테스트 디버깅 절차를 수행합니다.  
  
-   테스트할 데이터베이스의 개체에서 실행되는 하나 이상의 Transact\-SQL 스크립트. 이러한 Transact\-SQL 스크립트는 디버그할 수 없습니다.  
  
이 항목의 절차에서는 테스트할 데이터베이스의 저장 프로시저, 함수 및 트리거와 같은 특정 데이터베이스 개체를 디버깅하는 방법에 대해 설명합니다. 데이터베이스 개체를 디버깅하려면 아래 절차를 다음 순서대로 수행하십시오.  
  
1.  테스트 프로젝트에서 SQL Server 디버깅을 사용하도록 설정합니다.  
  
2.  테스트할 데이터베이스를 호스트하는 SQL Server 인스턴스에서 애플리케이션 디버깅을 사용하도록 설정합니다.  
  
3.  디버그할 데이터베이스 개체의 Transact\-SQL 스크립트에 중단점을 설정합니다.  
  
4.  단위 테스트를 디버깅합니다. 이 절차에서는 디버그 모드에서 테스트를 실행합니다.  
  
### <a name="to-enable-sql-debugging-on-your-test-project"></a>테스트 프로젝트에서 SQL 디버깅을 사용하도록 설정하려면  
  
1.  **솔루션 탐색기**를 엽니다.  
  
2.  **솔루션 탐색기**에서 테스트 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
    테스트 프로젝트와 동일한 이름의 속성 페이지가 열립니다.  
  
3.  속성 페이지에서 **디버그**를 클릭합니다.  
  
4.  **디버거 사용**에서 **SQL Server 디버깅 사용**을 클릭합니다.  
  
5.  변경 내용을 저장합니다.  
  
### <a name="to-set-an-increased-execution-context-timeout-to-enable-debugging-for-your-test-project"></a>테스트 프로젝트를 디버깅할 수 있도록 증가된 실행 컨텍스트 제한 시간을 설정하려면  
  
1.  **파일** 메뉴에서 **열기**를 가리키고 **파일**을 클릭합니다.  
  
2.  테스트 프로젝트가 들어 있는 폴더를 찾아 app.config 파일을 두 번 클릭 합니다.  
  
    app.config 파일이 편집기에서 열립니다.  
  
3.  다음 예제에서처럼 명령 제한 시간을 추가하도록 ExecutionContext 노드를 수정합니다.  
  
    ```  
    <ExecutionContext CommandTimeout ="300" Provider="System.Data.SqlClient" ConnectionString="Data Source=TargetServerName\TargetInstanceName;Initial Catalog=TargetDatabaseName;Integrated Security=True;Pooling=False" />  
    ```  
  
4.  변경 내용을 저장합니다.  
  
5.  단위 테스트 프로젝트를 다시 빌드합니다.  
  
> [!IMPORTANT]  
> 프로젝트를 다시 빌드하지 않으면 단위 테스트를 실행할 때 app.config에 대한 변경 내용이 적용되지 않으며 디버깅이 실패합니다.  
  
### <a name="to-add-breakpoints-to-your-transact-sql-script"></a>Transact\-SQL 스크립트에 중단점을 추가하려면  
  
1.  **보기** 메뉴에서 **SQL Server 개체 탐색기**를 엽니다.  
  
2.  **데이터 연결**에서 테스트할 데이터베이스의 노드를 확장합니다.  
  
3.  데이터베이스 아이콘 옆에 작은 빨간색 'x'가 나타나면 데이터베이스에 대한 연결이 닫혀 있는 것입니다. 이 경우에는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 클릭합니다. 데이터베이스에 대한 연결을 열려면 자격 증명을 제공해야 할 수 있습니다.  
  
4.  **보기**, **저장 프로시저** 또는 **함수** 노드를 확장하여 디버그할 개체를 찾습니다.  
  
5.  디버깅할 개체를 두 번 클릭합니다.  
  
6.  회색 세로 막대를 클릭하여 중단점을 설정합니다.  
  
### <a name="to-debug-your-sql-server-unit-test"></a>SQL Server 단위 테스트를 디버그하려면  
  
1.  Visual Studio 2010에서 **테스트 뷰** 창([테스트] -> [창])을 엽니다. Visual Studio 2012에서 **테스트 탐색기** 창을 엽니다.  
  
2.  중단점을 설정할 데이터베이스 개체를 실행하는 Transact\-SQL 스크립트가 있는 테스트를 마우스 오른쪽 단추로 클릭하고 **선택 항목 디버그**를 선택합니다.  
  
    데이터베이스 개체에서 중단점이 나타날 때까지 테스트가 디버그 모드에서 실행됩니다.  
  
3.  (옵션) 다른 디버그 창을 열려면 **디버그** 메뉴를 열고 **창**을 가리킨 후 **중단점**, **출력** 또는 **직접 실행**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 실행](../ssdt/running-sql-server-unit-tests.md)  
[Transact-SQL 디버깅(Visual Studio 2010)](https://go.microsoft.com/fwlink/?LinkId=163975)  
  

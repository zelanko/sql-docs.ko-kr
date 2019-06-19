---
title: SQL Server 단위 테스트 파일 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cee093c9-b97d-4fb0-b80f-806d071259dc
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9c595bd6d7cce21b9bf3428fadf772c4db4cdc07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65101918"
---
# <a name="sql-server-unit-test-files"></a>SQL Server 단위 테스트 파일
SQL Server 단위 테스트는 관리 코드에 대한 단위 테스트와 마찬가지로 테스트 프로젝트에 있습니다. **솔루션 탐색기**의 테스트 프로젝트 계층 구조에서 SQL Server 단위 테스트를 구성하는 항목을 볼 수 있습니다.  
  
SQL Server 단위 테스트는 몇 개의 파일에 포함된 여러 항목으로 구성됩니다. 다음 표에서는 SQL Server 단위 테스트를 구성하기 위해 상호 작용하는 파일에 대해 설명합니다.  
  
|**최근에 사용한 파일**|**설명**|  
|------------|-------------------|  
|.cs 또는 .vb|이 소스 코드 파일에는 [TestClass] 특성으로 데코레이트된 클래스가 포함되어 있습니다. 이 클래스에는 포함된 SQL Server 단위 테스트 각각에 대한 단일 테스트 메서드가 포함되어 있습니다. 이러한 메서드는 [TestMethod] 특성으로 데코레이팅됩니다.<br /><br />각 테스트 메서드에는 Transact\-SQL 테스트 스크립트를 실행하기에 적절한 코드가 포함되어 있습니다. 이 코드는 테스트 메서드를 만들 때 생성되며 이 코드를 수정할 수 있습니다.<br /><br />**참고:** **솔루션 탐색기**에서 이 파일을 두 번 클릭하면 SQL Server 단위 테스트 디자이너에서 테스트 클래스가 열립니다. .cs 또는 .vb 파일을 열어 해당 소스 코드를 보려면 **솔루션 탐색기**에서 파일을 마우스 오른쪽 단추로 클릭한 후 **코드 보기**를 클릭합니다.|  
|.resx|이 리소스 파일에는 연결된 .cs 또는 .vb 파일의 모든 테스트에 대한 Transact\-SQL 스크립트가 포함되어 있습니다. 이 스크립트 그룹에는 테스트 전 스크립트, 테스트 스크립트 및 테스트 후 스크립트가 포함되어 있습니다. 리소스 파일에는 편집할 수 있는 XML이 포함되어 있습니다. 리소스 파일은 테스트 어셈블리로 컴파일됩니다.<br /><br />**SQL Server 단위 테스트 디자이너**를 사용하여 Transact\-SQL 스크립트를 코딩해야 합니다. SQL Server 단위 테스트에 사용되는 스크립트에 대한 자세한 내용은 [SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)를 참조하세요.|  
|app.config|이 파일에는 명령 제한 시간 등의 다른 SQL Server 단위 테스트 구성 설정과 함께 테스트 프로젝트에 대한 데이터베이스 연결 문자열이 저장되어 있습니다. 자세한 내용은 [SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)를 참조하세요.|  
|SQLDatabaseSetup.cs 또는 SQLDatabaseSetup.vb|이 파일에는 테스트 프로젝트의 모든 SQL Server 단위 테스트에 대한 테스트 환경을 준비하는 클래스가 포함되어 있습니다. 이 클래스는 app.config 파일의 구성 설정을 기반으로 SQL Server 데이터베이스 프로젝트를 테스트 데이터베이스에 배포할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)  
  

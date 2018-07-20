---
title: 데이터베이스 단위 테스트가 포함된 이전 테스트 프로젝트 업그레이드 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42782ff3-e8cf-4c9d-8dac-a95b236edfc4
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7cfc482daed9c150079a8a5b29d32ee319f54745
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094747"
---
# <a name="upgrade-an-older-test-project-containing-database-unit-tests"></a>데이터베이스 단위 테스트가 포함된 이전 테스트 프로젝트 업그레이드
Visual Studio 2010에서 만들었고 데이터베이스 단위 테스트를 포함하는 이전 테스트 프로젝트를 업그레이드하여 새 SQL Server Data Tools 데이터베이스 단위 테스트 런타임 및 도구를 사용할 수 있습니다. 이전 프로젝트를 업그레이드한 후에는 프로젝트에 SQL Server 단위 테스트를 추가할 수 있습니다. 자세한 내용은 [SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)를 참조하세요.  
  
> [!TIP]  
> Visual Studio 2010을 사용하는 경우에는 테스트 프로젝트에 SQL Server 단위 테스트를 추가한 후 이전 데이터베이스 단위 테스트 템플릿을 사용하여 SQL Server 단위 테스트를 추가하면 안 됩니다. 그럴 경우 프로젝트를 다시 변환해야만 테스트가 올바르게 실행됩니다.  
  
Visual Studio 2010 이전 릴리스에서 만든 테스트 데이터베이스 프로젝트가 있는 경우 프로젝트를 Visual Studio 2010으로 업그레이드하기 전에 [방법: 이전 버전의 Visual Studio에서 데이터베이스 단위 테스트 업그레이드](http://msdn.microsoft.com/library/dd193412(VS.100).aspx)의 정보를 사용하여 데이터베이스 프로젝트를 SQL Server Data Tools로 업그레이드할 수 있습니다.  
  
### <a name="initiating-an-upgrade"></a>업그레이드 시작  
  
-   테스트 프로젝트에 대한 상황에 맞는 메뉴에서 프로젝트 업그레이드를 시작할 수 있습니다.  
  
    일부 경우에는 테스트 프로젝트 업그레이드를 시작할 수 있는 대화 상자가 SQL Server Data Tools에 표시됩니다.  
  
-   프로젝트를 업그레이드하면 이전 데이터베이스 테스트 프레임워크에 대한 어셈블리 참조가 제거되고 어댑터 어셈블리와 새 프레임워크에 대한 참조가 추가됩니다. app.config 파일도 업데이트됩니다.  
  
    > [!NOTE]  
    > 테스트 프로젝트에 DatabaseSetup 및 SQLDatabaseSetup 코드 파일이 모두 포함된 경우 프로젝트를 SQL Server Data Tools로 업그레이드하면 DatabaseSetup 파일이 빌드에서 제외됩니다. 빌드에서 제외된 경우 DatabaseSetup 파일을 제거할 수 있습니다.  
  
-   변환 후 이전 템플릿으로 만들어진 기존 데이터베이스 단위 테스트는 어댑터 어셈블리의 형식을 사용하여 새 프레임워크에 액세스합니다. 어댑터 어셈블리를 사용한다는 것은 업그레이드 과정에서 테스트 스크립트와 코드가 수정되지 않았음을 의미합니다. 프로젝트에 SQL Server 단위 테스트를 추가하면 새 테스트에서는 어댑터를 통하지 않고 직접 새 프레임워크를 참조합니다. 새 테스트와의 일관성을 위해 새 프레임워크를 사용하도록 기존 코드를 수동으로 업데이트할 수도 있지만 반드시 그럴 필요는 없습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  

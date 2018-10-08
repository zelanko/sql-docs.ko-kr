---
title: SQL Server 단위 테스트의 사용자 지정 테스트 조건 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 32a15d61-e908-4ae1-a238-4fd0f988d8c8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b136f2707012860ba7be88f61cd5f6de17ec148d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635891"
---
# <a name="custom-test-conditions--for-sql-server-unit-tests"></a>SQL Server 단위 테스트의 사용자 지정 테스트 조건
SQL Server 단위 테스트의 사용자 지정 테스트 조건을 추가할 수 있습니다. 그러나 사용자가 확장을 만들었든지 다른 사람이 만든 확장을 설치하려는 것이든지 관계없이 테스트 조건을 사용하려면 먼저 이를 설치해야 합니다.  
  
사용자가 만들지 않은 테스트 조건을 설치하려면 먼저 다음과 같은 위험 요소를 이해하고 있어야 합니다.  
  
-   테스트 조건의 설치 프로그램은 설치 권한을 기반으로 보호되는 리소스에 액세스하려고 하는 악의적 프로그램일 수 있습니다.  
  
-   테스트 조건 자체가 확장을 사용하는 사용자에게 충분한 사용 권한이 있는 경우 보호되는 리소스를 제어하려고 하는 악의적 프로그램일 수 있습니다.  
  
위험을 최소화하려면 출처를 알 수 있는 경우에만 사용자 지정 테스트 조건을 설치해야 합니다. 테스트 조건의 출처를 신뢰할 수 없는 경우에는 테스트 조건을 설치하기 전에 테스트 조건의 소스 코드와 해당 설치 프로그램(있는 경우)을 검사해야 합니다.  
  
사용자 지정 테스트 조건을 설치하려면 서명된 어셈블리(.dll)를 %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions 폴더에 복사합니다. 이 폴더가 없으면 새로 만듭니다. 이 디렉터리에 복사하려면 컴퓨터에 대한 관리 권한이 있어야 합니다.  
  
> [!NOTE]  
> 다음 경우에는 Visual Studio 2010 및 Visual Studio 2012 버전의 테스트 조건을 설치해야 합니다.  
>   
> -   SQL Server 단위 테스트를 빌드하는 데 사용될 수 있는 컴퓨터에 사용자 지정 테스트 조건을 설치하려는 경우  
> -   해당 단위 테스트가 Visual Studio 2010과 Visual Studio 2012에서 사용되는 경우  
  
SQL Server 단위 테스트의 사용자 지정 테스트 조건에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [방법: SQL Server 단위 테스트 디자이너용 테스트 조건 만들기](../ssdt/how-to-create-test-conditions-for-the-sql-server-unit-test-designer.md)  
  
-   [방법: 이전 릴리스의 Visual Studio 2010 사용자 지정 테스트 조건을 SQL Server Data Tools로 업그레이드](../ssdt/how-to-upgrade-visual-studio-2010-custom-test-condition-to-ssdt.md)  
  
-   [연습: 사용자 지정 테스트 조건을 사용하여 저장 프로시저 결과 확인](../ssdt/walkthrough-use-custom-test-condition-to-verify-stored-procedure-results.md)  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  

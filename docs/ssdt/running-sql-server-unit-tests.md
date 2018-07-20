---
title: SQL Server 단위 테스트 실행 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.data.tools.unittesting.testconfig
ms.assetid: febcc87f-eb18-4c12-ba30-82ef0d49aaa3
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c8ae9faa2a1556b7ca1e71c7cc52e00df2222688
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094931"
---
# <a name="running-sql-server-unit-tests"></a>SQL Server 단위 테스트 실행
코드 품질을 향상하고 유지 관리하기 위해 데이터베이스 개체의 동작을 확인하는 SQL Server 단위 테스트를 만들어 실행한 후 해당 테스트를 버전 제어에 체크 인할 수 있습니다. 사용자 본인이나 팀의 멤버가 데이터베이스 스키마를 변경하는 경우 SQL Server 단위 테스트와 소프트웨어 단위 테스트를 모두 실행하여 변경 내용으로 인해 기존 기능이 손상되지 않았는지 확인해야 합니다. 개별 테스트를 실행하거나 테스트 목록이라고 하는 테스트 그룹을 실행할 수 있습니다. 자세한 내용은 [테스트 목록 사용(Visual Studio 2010)](http://msdn.microsoft.com/library/ms182461(VS.100).aspx)을 참조하세요.  
  
## <a name="ways-to-run-sql-server-unit-tests"></a>SQL Server 단위 테스트를 실행하는 방법  
아래에서 보여 주는 것과 같이 설치한 소프트웨어에 따라 다른 여러 가지 방법으로 SQL Server 단위 테스트를 실행할 수 있습니다.  
  
-   Visual Studio 2010 **테스트 뷰** 창을 사용하여 테스트를 실행합니다. 자세한 내용은 [방법: SQL Server 단위 테스트 실행](../ssdt/how-to-run-sql-server-unit-tests.md) 및 [방법: Microsoft Visual Studio 2010에서 자동화된 테스트 실행](http://msdn.microsoft.com/library/ms182470(VS.100).aspx)을 참조하세요. Visual Studio 2012의 경우에는 [방법: Microsoft Visual Studio 2012에서 자동화된 테스트 실행](http://msdn.microsoft.com/library/ms182470.aspx)을 참조하세요.  
  
-   명령 프롬프트에서 MSTest.exe 명령을 사용하여 테스트를 실행합니다. 자세한 내용은 [방법: MSTest를 사용하여 명령줄에서 자동화된 테스트 실행(Visual Studio 2010)](http://msdn.microsoft.com/library/ms182487(VS.100).aspx) 또는 [MSTest를 사용하여 명령줄에서 자동화된 테스트 실행(Visual Studio 2012)](http://msdn.microsoft.com/library/ms182487.aspx)을 참조하세요.  
  
-   테스트 프로젝트를 실행하여 **솔루션 탐색기**에서 테스트를 실행합니다. 자세한 내용은 [방법: Microsoft Visual Studio 2010에서 자동화된 테스트 실행](http://msdn.microsoft.com/library/ms182470(VS.100).aspx) 또는 [방법: Microsoft Visual Studio 2012에서 자동화된 테스트 실행](http://msdn.microsoft.com/library/ms182470.aspx)을 참조하세요.  
  
-   **테스트 결과** 창에서 테스트를 다시 실행합니다. 자세한 내용은 [방법: 테스트 다시 실행(Visual Studio 2010)](http://msdn.microsoft.com/library/ms182472(VS.100).aspx)을 참조하세요.  
  
-   **테스트 목록 편집기** 창에서 테스트 목록을 실행하거나 개별 테스트를 실행합니다(Visual Studio 2010). 자세한 내용은 [방법: Microsoft Visual Studio 2010에서 자동화된 테스트 실행](http://msdn.microsoft.com/library/ms182470(VS.100).aspx) 또는 [방법: Microsoft Visual Studio 2012에서 자동화된 테스트 실행](http://msdn.microsoft.com/library/ms182470.aspx)을 참조하세요.  
  
-   Team Foundation Build에서 프로젝트를 빌드할 때 테스트를 실행합니다. 자세한 내용은 [방법: 응용 프로그램을 빌드한 후 예약된 테스트 구성 및 실행(Visual Studio 2010)](http://msdn.microsoft.com/library/ms182465(VS.100).aspx) 또는 [방법: 응용 프로그램을 빌드한 후 예약된 테스트 구성 및 실행(Visual Studio 2012)](http://msdn.microsoft.com/library/ms182465.aspx)을 참조하세요.  
  
순서가 지정된 테스트를 사용하여 SQL Server 단위 테스트를 특정 순서로 실행할 수 있습니다. 자세한 내용은 [방법: 순서가 지정된 테스트 만들기(Visual Studio 2010)](http://msdn.microsoft.com/library/ms182631(VS.100).aspx) 또는 [방법: 순서가 지정된 테스트 만들기(Visual Studio 2012)](http://msdn.microsoft.com/library/ms182631.aspx)를 참조하세요.  
  
## <a name="interpreting-tests-results"></a>테스트 결과 해석  
테스트를 실행하면 **테스트 결과** 창에 통과한 테스트 또는 실패한 테스트가 표시됩니다. 자세한 내용은 [SQL Server 단위 테스트 결과 해석](../ssdt/interpreting-sql-server-unit-test-results.md)을 참조하세요. 예기치 않은 오류를 진단하는 방법에 대한 자세한 내용은 [방법: 데이터베이스 개체 디버그](../ssdt/how-to-debug-database-objects.md)를 참조하세요.  
  
## <a name="topics-in-this-section"></a>이 섹션의 항목  
이 섹션에서는 다음 항목을 다룹니다.  
  
-   [방법: 데이터베이스 개체 디버그](../ssdt/how-to-debug-database-objects.md)  
  
-   [방법: Team Foundation Build에서 SQL Server 단위 테스트 실행](../ssdt/how-to-run-sql-server-unit-tests-from-team-foundation-build.md)  
  
-   [방법: SQL Server 단위 테스트 실행](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
-   [SQL Server 단위 테스트 결과 해석](../ssdt/interpreting-sql-server-unit-test-results.md)  
  
## <a name="related-scenarios"></a>관련 시나리오  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
단위 테스트를 정의하여 데이터베이스 개체의 동작을 확인하고 각 테스트 프로젝트를 다른 데이터 생성 계획, 배포 구성 및 연결 문자열과 연결할 수 있습니다.  
  
[SQL Server 단위 테스트의 사용자 지정 테스트 조건](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
사용자 지정 테스트 조건을 만들면 기본 테스트 조건으로는 확인할 수 없는 조건에 대해 테스트할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  

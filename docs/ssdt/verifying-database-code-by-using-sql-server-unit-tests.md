---
title: SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 003713e2-de6b-4277-a0a8-7d1f2f4ffb39
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b3e720389f790282f1ad7a33302e2d277128178f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140948"
---
# <a name="verifying-database-code-by-using-sql-server-unit-tests"></a>SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인
SQL Server 단위 테스트를 사용하면 데이터베이스의 기준 상태를 설정하고 이후 데이터베이스 개체에 대해 수행하는 변경 내용을 확인할 수 있습니다.  
  
데이터베이스의 기준 상태를 설정하려면 테스트 프로젝트를 만들고 데이터베이스 개체에 대해 실행되는 Transact\-SQL 집합을 작성합니다. 이러한 테스트를 사용하여 격리된 개발 환경에서 해당 개체가 예상대로 작동하는지 여부를 확인할 수 있습니다. SQL Server 단위 테스트는 SQL Server 데이터베이스 프로젝트를 사용하는 오프라인 데이터베이스 개발에서 수행하면 효과적입니다(자세한 내용은 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 참조). SQL Server 단위 테스트의 기준 집합이 준비되었으면 변경 내용을 버전 제어에 체크 인하기 전에 이러한 테스트를 사용하여 데이터베이스가 올바르게 작동하는지 확인할 수 있습니다.  
  
데이터베이스 개체에 대한 변경 내용을 확인하는 테스트를 만들 수 있습니다. 또한 데이터베이스 함수, 트리거 및 저장 프로시저를 테스트하는 Transact\-SQL 코드 스텁을 자동으로 생성할 수 있습니다.  
  
> [!NOTE]  
> SQL Server 단위 테스트는 데이터베이스 프로젝트를 열지 않고도 만들고 실행할 수 있습니다. 하지만 프로젝트에서 특정 데이터베이스 개체를 테스트하기 위한 테스트 스크립트를 자동으로 생성하려면 테스트하려는 개체가 포함된 데이터베이스 프로젝트를 열어야 합니다.  
  
사용자 또는 사용자의 팀 멤버가 데이터베이스 스키마를 변경할 경우 이러한 테스트를 사용해서 해당 변경 내용으로 인해 기존 기능이 중단되었는지 여부를 확인할 수 있습니다. SQL Server 단위 테스트는 소프트웨어 개발자가 만드는 SQL Server 단위 테스트를 보완하기 위해 만듭니다. 애플리케이션의 전체 동작을 확인하려면 두 가지 테스트 집합을 모두 완료해야 합니다.  
  
단위 테스트를 사용하면 프로시저가 성공해야 할 때 성공하고 실패해야 할 때 실패하는지를 확인할 수 있습니다. 실패가 올바르게 발생하는지 확인하는 테스트를 부정 테스트라고 부릅니다.  
  
## <a name="visual-studio-editions-support-for-sql-server-unit-tests"></a>Visual Studio 버전의 SQL Server 단위 테스트 지원  
SQL Server Data Tools의 2012년 12월 업데이트에 추가된 SQL Server 단위 테스트 기능을 사용하면 Visual Studio 2010 Professional 및 Visual Studio 2012 Professional 이상의 버전에서 SQL Server 단위 테스트를 만들고 수정하고 실행할 수 있습니다.  
  
최신 SQL Server Data Tools 업데이트를 설치하려면 [업데이트 확인 대화 상자](../ssdt/check-for-updates-dialog-box.md)에 액세스합니다.  
  
Visual Studio 2010 및 Visual Studio 2012 통합 SQL Server Data Tools 셸은 SQL Server 단위 테스트를 지원하지 않습니다.  
  
## <a name="common-tasks"></a>일반 태스크  
다음 표에서는 이 시나리오를 지원하는 일반 태스크에 대한 설명과 이러한 태스크를 성공적으로 완료하기 위한 자세한 방법에 대한 링크를 제공합니다.  
  
|일반 태스크|지원 콘텐츠|  
|----------------|----------------------|  
|**실습 가져오기:** 기능 소개 연습에 따라 간단한 SQL Server 단위 테스트를 만들고 실행하는 방법에 익숙해질 수 있습니다. 이 연습에는 부정 SQL Server 단위 테스트 예도 포함됩니다.|[연습: SQL Server 단위 테스트 만들기 및 실행](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**SQL Server 단위 테스트 정의:** 자신의 프로젝트에서 SQL Server 단위 테스트를 만들어야 합니다. 해당 프로젝트에 대한 설정을 구성하고 각 테스트에 대해 하나 이상의 테스트 조건을 정의합니다.|[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)<br /><br />[SQL Server 단위 테스트에서 테스트 조건 사용](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)|  
|**SQL Server 단위 테스트 실행:** 하나 이상의 단위 테스트를 정의한 후 이를 실행하고, 문제를 디버그하고, 테스트 결과를 검사합니다.|[SQL Server 단위 테스트 실행](../ssdt/running-sql-server-unit-tests.md)|  
|**테스트 그룹 관리(Visual Studio 2010):** 일반적으로 동시에 실행해야 하는 테스트는 그룹으로 구성할 수 있습니다. 테스트 목록은 계속 지원되지만 새로운 테스트 그룹의 경우 대신 테스트 범주를 사용해야 합니다. 예를 들어 특정 ‘스키마’의 모든 개체 또는 트리거의 테스트에 대해 테스트 범주를 만들 수 있습니다. |[테스트 그룹 지정을 위한 테스트 범주 정의](https://msdn.microsoft.com/library/dd286595(VS.100).aspx)<br /><br />[테스트 그룹 지정을 위한 테스트 목록 정의](https://msdn.microsoft.com/library/dd286584(VS.100).aspx)|  
|**테스트 프로젝트 및 테스트를 버전 제어에서 확인:** 테스트를 실행하고 올바르게 작동하는지 확인한 후에는 모든 팀 멤버가 테스트를 실행할 수 있도록 테스트 프로젝트 및 모든 관련 파일을 버전 제어에서 확인해야 합니다. 테스트 프로젝트를 SQL Server 데이터베이스 프로젝트와 함께 버전 제어에 체크 인하면 데이터베이스와 데이터베이스 테스트 모두의 호환되는 버전을 쉽게 복원할 수 있습니다.|[버전 제어에 파일 추가](https://msdn.microsoft.com/library/ms181374(VS.100).aspx)<br /><br />[체크 인 및 보류 중인 변경 내용 창 사용](https://msdn.microsoft.com/library/ms245462(VS.100).aspx)|  
|**사용자 지정 테스트 조건 정의:** 기본 테스트 조건 세트에 포함되지 않는 동작을 테스트해야 할 경우에는 사용자 지정 테스트 조건을 만들 수 있습니다. 이러한 조건은 새 조건을 사용하는 테스트를 실행하기 원하는 모든 팀 멤버에게 배포해야 합니다.|[시나리오: SQL Server 단위 테스트에 대한 사용자 지정 테스트 조건 정의](https://msdn.microsoft.com/library/dd193282(VS.100).aspx)|  
|**기존 단위 테스트 업데이트:** 이전 버전의 Visual Studio에서 만든 데이터베이스 단위 테스트를 이 릴리스에서 성공적으로 빌드하고 실행하기 위해서는 업그레이드해야 합니다.<br /><br />**참고:** 이전 버전의 Visual Studio에서 만든 데이터베이스 단위 테스트 프로젝트와 데이터베이스 프로젝트가 모두 포함된 솔루션을 열면 데이터베이스 프로젝트를 업그레이드하라는 메시지가 표시됩니다. 데이터베이스 단위 테스트 프로젝트를 업그레이드하라는 메시지는 표시되지 않으며 이러한 프로젝트는 수동으로 업그레이드해야 합니다.|[데이터베이스 단위 테스트가 포함된 이전 테스트 프로젝트 업그레이드](../ssdt/upgrade-an-older-test-project-containing-database-unit-tests.md)|  
|**확장성:** 기능 확장을 만들어 SQL Server Data Tools를 확장할 수 있습니다.|[SQL Server 단위 테스트의 사용자 지정 테스트 조건](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)|  
|**문제 해결**: SQL Server 단위 테스트와 관련된 일반적인 문제를 해결하는 방법을 자세히 알아볼 수 있습니다.|[SQL Server 데이터베이스 단위 테스트 문제 해결](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>관련 시나리오  
[프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md)  
데이터베이스 단위 테스트는 SQL Server 데이터베이스 프로젝트를 사용한 오프라인 프로젝트 개발과 함께 사용할 경우 특히 효과적입니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
  

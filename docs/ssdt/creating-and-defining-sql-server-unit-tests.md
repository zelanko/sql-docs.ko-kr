---
title: SQL Server 단위 테스트 만들기 및 정의 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.DatabaseMethodNameDialog
- sql.data.tools.unittesting.designer
ms.assetid: 3c082177-a2b1-4fde-8833-b49b2a351815
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b52fc60f3102e7b6a38d254fba682ab4321d804
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088335"
---
# <a name="creating-and-defining-sql-server-unit-tests"></a>SQL Server 단위 테스트 만들기 및 정의
SQL Server 단위 테스트를 실행하면 스키마에 있는 하나 이상의 데이터베이스 개체에 대한 변경 내용으로 인해 데이터베이스 응용 프로그램의 기존 기능이 중단되는지 여부를 확인할 수 있습니다. 이러한 테스트는 소프트웨어 개발자가 만드는 단위 테스트를 보완합니다. 응용 프로그램의 동작을 확인하려면 두 가지 테스트 유형을 모두 실행해야 합니다.  
  
SQL Server 단위 테스트를 추가하고 스키마의 개체를 테스트하는 Transact\-SQL 스크립트를 추가하여 해당 개체의 동작을 확인할 수 있습니다. 또 다른 방법으로, 특정 함수, 트리거 또는 저장 프로시저의 동작을 확인하려는 경우에는 Transact\-SQL 스크립트의 스텁을 자동으로 생성할 수 있습니다. 스텁을 생성한 후에는 의미 있는 결과를 얻기 위해 사용자 지정할 수 있습니다.  
  
> [!NOTE]  
> SQL Server 데이터베이스 프로젝트를 열지 않고도 비어 있는 테스트를 만들고, 여기에 코드를 추가하고, 테스트를 실행할 수 있습니다. 하지만 테스트하려는 개체가 포함된 프로젝트를 열지 않으면 함수, 트리거 또는 저장 프로시저를 테스트하는 Transact\-SQL 스텁을 자동으로 생성할 수 없습니다.  
  
## <a name="common-tasks"></a>일반 태스크  
다음 표에서는 이 시나리오를 지원하는 일반 태스크에 대한 설명과 이러한 태스크를 성공적으로 완료하기 위한 자세한 방법에 대한 링크를 제공합니다.  
  
|일반 태스크|지원 콘텐츠|  
|----------------|----------------------|  
|**실습 가져오기**: 기능 소개 연습에 따라 간단한 SQL Server 단위 테스트를 만들고 실행하는 방법에 익숙해질 수 있습니다.|-   [연습: SQL Server 단위 테스트 만들기 및 실행](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)|  
|**SQL Server 단위 테스트에 대해 자세히 알아보기**: SQL Server 단위 테스트를 구성하는 파일 및 스크립트에 대해 자세히 알아볼 수 있습니다. 또한 SQL Server 단위 테스트에서 테스트 조건 및 Transact\-SQL 어설션을 사용하는 방법도 확인할 수 있습니다.|-   [SQL Server 단위 테스트의 스크립트](../ssdt/scripts-in-sql-server-unit-tests.md)<br />-   [SQL Server 단위 테스트 파일](../ssdt/sql-server-unit-test-files.md)<br />-   [SQL Server 단위 테스트에서 테스트 조건 사용](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)<br />-   [SQL Server 단위 테스트에서 Transact-SQL 어설션 사용](../ssdt/using-transact-sql-assertions-in-sql-server-unit-tests.md)|  
|**하나 이상의 테스트 프로젝트 만들기**: 테스트 프로젝트에서 SQL Server 단위 테스트를 만들어야 합니다. 테스트 프로젝트를 만들기 전에 SQL Server 개체 탐색기를 사용하여 SQL Server 단위 테스트를 만들면 테스트 프로젝트가 자동으로 만들어집니다. 각 테스트 집합에서 서로 다른 데이터 생성 계획이나 서로 다른 배포 구성을 사용하려는 경우 등에는 테스트 프로젝트를 둘 이상 만들 수 있습니다. 테스트 프로젝트를 만들 때는 해당 프로젝트에 사용할 테스트 설정(예: 연결 문자열), 배포 설정 및 데이터 생성 계획을 구성할 수 있습니다.|-   [방법: SQL Server 데이터베이스 단위 테스트용 테스트 프로젝트 만들기](../ssdt/how-to-create-a-test-project-for-sql-server-database-unit-testing.md)<br />-|  
|**단위 테스트 실행 방법 구성**: 테스트를 실행할 데이터베이스에 대한 연결 문자열, 데이터 생성 계획 및 배포 설정을 지정할 수 있습니다. 이러한 설정은 프로젝트에 SQL Server 단위 테스트를 처음 추가할 때 구성하지만 이를 나중에 수정할 수도 있습니다.|-   [방법: SQL Server 단위 테스트 실행 구성](../ssdt/how-to-configure-sql-server-unit-test-execution.md)<br />-   [연결 문자열 및 사용 권한 개요](../ssdt/overview-of-connection-strings-and-permissions.md)|  
|**SQL Server 단위 테스트 만들기**: 함수, 트리거 또는 저장 프로시저의 동작을 확인하는 SQL Server 단위 테스트에 대한 Transact\-SQL 코드 스텁을 자동으로 만들 수 있습니다. 또한 비어 있는 SQL Server 단위 테스트를 만든 다음, 다른 데이터베이스 개체 유형을 테스트하도록 Transact\-SQL 코드를 추가할 수도 있습니다.|-   [방법: 함수, 트리거 및 저장 프로시저에 대한 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)<br />-   [방법: 빈 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)|  
|**SQL Server 단위 테스트에 대한 코드 작성**:SQL Server 단위 테스트를 만든 후에는 데이터베이스 개체를 테스트하도록 Transact\-SQL 코드를 수정하거나 작성합니다. 각 테스트에 대해 테스트가 통과 또는 실패할지를 결정하는 하나 이상의 테스트 조건을 정의합니다. 보다 복잡한 테스트의 경우 데이터베이스 프로젝트에서 Visual Basic 또는 Visual C\# 코드를 수정할 수 있습니다. 예를 들어 단일 트랜잭션 범위에서 실행되는 단위 테스트를 작성할 수 있습니다.|-   [방법: 편집할 SQL Server 단위 테스트 열기](../ssdt/how-to-open-a-sql-server-unit-test-to-edit.md)<br />-   [방법: SQL Server 단위 테스트에 테스트 조건 추가](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)<br />-   [방법: 단일 트랜잭션 범위 내에서 실행되는 SQL Server 단위 테스트 작성](../ssdt/how-to-write-sql-server-unit-test-that-runs-in-single-transaction-scope.md)<br />-   [SQL Server 단위 테스트 디자이너의 바로 가기 키](../ssdt/keyboard-shortcuts-for-sql-server-unit-test-designer.md)|  
|**문제 해결**: SQL Server와 관련된 일반적인 문제를 해결하는 방법을 자세히 확인할 수 있습니다.|-   [SQL Server 데이터베이스 단위 테스트 문제 해결](../ssdt/troubleshooting-sql-server-database-unit-testing-issues.md)|  
  
## <a name="related-scenarios"></a>관련 시나리오  
[SQL Server 단위 테스트 실행](../ssdt/running-sql-server-unit-tests.md)  
SQL Server 단위 테스트를 만든 후에는 [테스트 뷰] 창이나 SQL Server 단위 테스트 디자이너에서 또는 Team Foundation Build를 사용하여 실행할 수 있습니다.  
  
[시나리오: 데이터베이스 단위 테스트의 사용자 지정 테스트 조건 정의](http://msdn.microsoft.com/library/dd193282(VS.100).aspx)  
기본 테스트 조건으로 확인할 수 없는 동작을 테스트하기 위해 사용자 지정 테스트 조건을 만들 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  

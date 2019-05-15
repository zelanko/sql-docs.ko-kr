---
title: SQL Server Data Tools | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.errortask.generichelp
ms.assetid: 5f08f15a-851d-4026-a557-28b3c6492efe
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9ea53ad33b58d7c838017dd2761e74a780214bb0
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65101872"
---
# <a name="sql-server-data-tools"></a>SQL Server Data Tools
SSDT(SQL Server Data Tools)에서는 Visual Studio 내의 모든 데이터베이스 개발 단계를 망라하는 선언적 유비쿼터스 모델을 도입함으로써 데이터베이스 개발 과정에 일대 변화를 주었습니다. SSDT Transact\-SQL 디자인 기능을 사용하여 데이터베이스를 빌드, 디버깅, 유지 관리 및 리팩터링할 수 있습니다. 데이터베이스 프로젝트를 사용하여 작업하거나 내부 또는 외부의 연결된 데이터베이스 인스턴스를 직접 사용할 수 있습니다.  
  
개발자는 데이터베이스 개발에 익숙한 Visual Studio 도구를 사용할 수 있습니다. Transact\-SQL 편집기에서는 C# 및 Visual Basic에 사용할 수 있는 기능과 유사한 코드 탐색, IntelliSense 및 언어 지원과 같은 도구, 플랫폼별 유효성 검사, 디버깅 및 선언적 편집 기능을 제공합니다. 또한 SSDT에서는 데이터베이스 프로젝트나 연결된 데이터베이스 인스턴스에서 테이블을 만들고 편집하는 데 사용할 수 있는 시각적 테이블 디자이너를 제공합니다. 팀 기반 환경에서 데이터베이스 프로젝트 작업을 수행하는 동안 모든 파일에 대해 버전 제어를 사용할 수 있습니다. 프로젝트를 게시할 때 SQL Database 및 SQL 서버를 포함하여 지원되는 모든 SQL 플랫폼에 게시할 수 있습니다. SSDT 플랫폼 유효성 검사 기능은 스크립트가 지정한 대상에서 작동하도록 해 줍니다.  
  
Visual Studio의 SQL Server 개체 탐색기에서는 SQL Server Management Studio와 유사한 데이터베이스 개체의 뷰를 제공합니다. SQL Server 개체 탐색기를 사용하여 소규모 데이터베이스 관리 및 디자인 작업을 수행할 수 있습니다. 테이블, 저장 프로시저 및 함수를 손쉽게 만들고, 편집하고, 이름을 바꾸고 삭제할 수 있을 뿐 아니라, SQL Server 개체 탐색기에서 바로 상황에 맞는 메뉴를 사용하여 테이블 데이터를 편집하거나, 스키마를 비교하거나, 쿼리를 실행할 수도 있습니다.  
  
다음 항목과 섹션에서는 SSDT를 유용하게 사용할 수 있는 방법에 대해 설명합니다. 데이터베이스 프로젝트 작업을 완료할 수 있도록 안내하는 방법 도움말 항목이 포함되어 있습니다. 이러한 작업은 자습서처럼 순서대로 완료하도록 작성되었으며, 전문 식품을 수입 및 수출하는 가상의 회사인 Northwind Traders를 중심으로 설명합니다.  
  
|항목/섹션|설명|  
|-------------------|---------------|  
|[프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md)|이 섹션의 항목에서는 데이터베이스 프로젝트를 작성, 빌드, 디버그 및 게시하는 데 사용할 수 있는 SQL Server Data Tools 기능에 대해 설명합니다.|  
|[명령줄 도구를 사용하여 프로젝트 기반 데이터베이스 개발](../ssdt/project-oriented-database-development-using-command-line-tools.md)|이 섹션의 항목에서는 많은 프로젝트 기반 데이터베이스 개발 시나리오를 활성화하는 명령줄 도구에 대해 설명합니다.|  
|[연결된 데이터베이스 개발](../ssdt/connected-database-development.md)|이 섹션의 항목에서는 연결된 데이터베이스를 디자인하고 쿼리하는 데 사용하는 SQL Server Data Tools 기능에 대해 설명합니다.|  
|[하나 이상의 테이블에 있는 데이터를 참조 데이터베이스에 있는 데이터와 비교 및 동기화](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)|원본 데이터베이스와 대상 데이터베이스의 데이터를 비교하고 일치해야 하는 값을 지정한 후 대상을 업데이트하여 데이터베이스를 동기화하거나 업데이트 스크립트를 Transact\-SQL 편집기 또는 파일로 내보내는 방법에 대해 설명합니다.|  
|[Transact-SQL 편집기를 사용하여 스크립트 편집 및 실행](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)|이 섹션의 항목에서는 스크립트 작업에 사용할 수 있는 다양한 기능의 편집 및 디버깅 환경을 제공하는 Transact\-SQL 편집기의 사용 방법에 대해 설명합니다.|  
|[테이블 및 관계 관리, 오류 해결](../ssdt/manage-tables-relationships-and-fix-errors.md)|이 섹션의 항목에서는 다음 내용에 대해 설명합니다.<br /><br />-   테이블 디자이너를 사용하여 테이블을 디자인하고 테이블 관계를 관리하는 방법<br />-   일반적인 구문 또는 의미 오류를 해결하는 방법|  
|[SQL Server 단위 테스트를 사용하여 데이터베이스 코드 확인](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)|SQL Server 단위 테스트를 사용하여 데이터베이스의 기준 상태를 설정하고 이후 데이터베이스 개체에 대해 수행하는 변경 내용을 확인하는 방법에 대해 설명합니다.|  
|[데이터베이스 기능 확장](../ssdt/extending-the-database-features.md)|단위 테스트 및 데이터베이스 코드 분석과 같은 기능을 확장할 수 있도록 하는 기능 확장을 만들 수 있습니다.|  
|[SQL Server Data Tools에 필요한 권한](../ssdt/required-permissions-for-sql-server-data-tools.md)|SQL Server Data Tools를 사용하는 데 필요한 액세스 권한에 대해 설명합니다.|  
|[DAC 프레임워크 호환성](../ssdt/dac-framework-compatibility.md)|DAC 프레임워크와의 호환성 문제를 설명합니다.|  
  

  

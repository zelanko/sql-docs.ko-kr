---
title: 프로젝트 기반 오프라인 데이터베이스 개발 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbprojectwizard.general
- sql.data.tools.dbprojectwizard.summary
ms.assetid: e61e830d-9fcd-45e7-b7b4-93a42155dd56
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96effd7670d22461f6c347c9220f7a3c26b7f611
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624521"
---
# <a name="project-oriented-offline-database-development"></a>프로젝트 기반 오프라인 데이터베이스 개발
이 섹션에서는 데이터베이스 프로젝트를 작성, 빌드, 디버깅 및 게시하는 데 사용할 수 있는 SSDT(SQL Server Data Tools)의 기능에 대해 설명합니다.  
  
SSDT를 사용하여 서버 인스턴스에 연결하지 않고도 오프라인 데이터베이스 프로젝트를 만들고 프로젝트의 개체 정의(스크립트로 표시됨)를 추가, 수정 또는 삭제하여 스키마 변경을 구현할 수 있습니다. 이러한 작업은 모두 테이블 디자이너나 Transact\-SQL 편집기를 사용하여 수행할 수 있습니다. 동일한 프로젝트에서 Transact\-SQL 및 CLR 개체를 작성하고 디버그할 수도 있습니다. 스키마 비교를 사용하면 프로젝트를 프로덕션 데이터베이스와 동기화 상태로 유지하고, 비교를 위해 개발 주기의 각 단계에서 프로젝트의 스냅숏을 만들 수 있습니다. 팀 기반 환경에서 데이터베이스 프로젝트 작업을 수행하는 동안 모든 파일에 대해 버전 제어를 사용할 수 있습니다. 데이터베이스 프로젝트를 개발, 테스트 및 디버깅한 후 권한이 있는 사용자에게 프로젝트를 전달하여 프로덕션 환경에 게시하도록 할 수 있습니다.  
  
> [!NOTE]  
> 이 섹션의 방법 도움말 항목에는 순서대로 완료할 수 있는 일련의 작업이 포함되어 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|---------|---------------|  
|[데이터베이스 프로젝트로 가져오기](../ssdt/import-into-a-database-project.md)|라이브 데이터베이스, .dacpac 또는 스크립트에서 개체 가져오기에 대해 설명합니다.|  
|[데이터베이스 참조 추가 대화 상자](../ssdt/add-database-reference-dialog-box.md)|데이터베이스 참조를 추가하기 위한 다양한 방법에 대해 설명합니다.|  
|[업데이트 확인 대화 상자](../ssdt/check-for-updates-dialog-box.md)|SQL Server Data Tools에서 제품 업데이트를 확인하는 방법에 대해 설명합니다.|  
|[데이터베이스 프로젝트 설정](../ssdt/database-project-settings.md)|데이터베이스 및 빌드 구성의 여러 측면을 제어하기 위한 다양한 프로젝트 설정에 대해 설명합니다.|  
|[방법: SQL Server 데이터베이스 프로젝트의 개체 찾아보기](../ssdt/how-to-browse-objects-in-a-sql-server-database-project.md)|이제 Visual Studio의 SQL Server 개체 탐색기에는 솔루션의 모든 SQL Server 데이터베이스 프로젝트가 SQL Server Management Studio와 유사한 계층 구조로 그룹화되는 전용 프로젝트 노드가 포함되어 있습니다.|  
|[Data Tools 작업 창](../ssdt/data-tools-operations-window.md)|일부 작업의 진행률을 표시하고 오류가 발생하는 경우 알림을 표시하는 **데이터 도구 작업** 창에 대해 설명합니다.|  
|[Transact-SQL 편집기 옵션](../ssdt/transact-sql-editor-options.md)|Transact\-SQL 옵션에 대해 설명합니다.|  
|[방법: 새 데이터베이스 프로젝트 만들기](../ssdt/how-to-create-a-new-database-project.md)|데이터베이스 프로젝트를 만들고 기존 데이터베이스 스키마를 가져옵니다.|  
|[방법: 스키마 비교를 사용하여 서로 다른 데이터베이스 정의 비교](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)|데이터베이스와 프로젝트의 스키마를 비교하고 동기화합니다.|  
|[방법: 로컬 데이터베이스 빌드 및 배포](../ssdt/how-to-build-and-deploy-to-a-local-database.md)|데이터베이스 프로젝트를 디버그할 때 활성화되는 로컬 주문형 SQL Server 인스턴스를 사용합니다.|  
|[방법: 대상 플랫폼 변경 및 데이터베이스 프로젝트 게시](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)|프로젝트의 대상 SQL Server 플랫폼을 지원되는 SQL Server 인스턴스로 변경하고 구문의 유효성을 검사합니다.|  
|[방법: 프로젝트의 스냅숏 만들기](../ssdt/how-to-create-a-snapshot-of-a-project.md)|데이터베이스 스키마의 읽기 전용 프록시를 만들고, 원하지 않는 변경 내용이 프로젝트에 적용된 경우 원본 프로젝트로 되돌립니다.|  
|[방법: 프로젝트에서 Microsoft SQL Server 2012 개체 사용](../ssdt/how-to-use-microsoft-sql-server-2012-objects-in-your-project.md)|프로젝트에 새 시퀀스 개체를 추가합니다.|  
|[방법: CLR 데이터베이스 개체 작업](../ssdt/how-to-work-with-clr-database-objects.md)|SQL Server Data Tools 데이터베이스 프로젝트에 CLR 개체를 만들고 게시합니다.|  
|[방법: Visual Studio 2010 데이터베이스 프로젝트를 SQL Server 데이터베이스 프로젝트로 변환 및 다른 플랫폼으로 대상 변경](../ssdt/how-to-convert-visual-studio-2010-database-projects-to-ssql-server-projects.md)|Visual Studio 2010에서 만든 기존의 SQL Server 데이터베이스, CLR 개체 및 데이터 계층 애플리케이션 프로젝트를 SQL Server Data Tools 데이터베이스 프로젝트로 변환할 수 있습니다.|  
|[방법: 배포 전 또는 배포 후 스크립트 지정](../ssdt/how-to-specify-predeployment-or-postdeployment-scripts.md)|데이터베이스를 배포하기 전이나 후에 실행하려는 스크립트를 사용하는 방법에 대해 설명합니다.|  
  
## <a name="related-sections"></a>관련 섹션  
[테이블 및 관계 관리, 오류 해결](../ssdt/manage-tables-relationships-and-fix-errors.md)  
  

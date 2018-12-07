---
title: '방법: 대상 플랫폼 변경 및 데이터베이스 프로젝트 게시 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.publish.dialog
- sql.data.tools.publishdacproject
ms.assetid: 6012e120-5f72-4f4f-ae6e-f9a57ae1dea7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5dc61811562a8c9fb121d170d89b0b28806b29f4
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516705"
---
# <a name="how-to-change-target-platform-and-publish-a-database-project"></a>방법: 대상 플랫폼 변경 및 데이터베이스 프로젝트 게시
SSDT(SQL Server Data Tools) 데이터베이스 프로젝트의 대상 SQL Server 버전을 지원되는 SQL Server 인스턴스(SQL Server 2005, 2008, 2008 R2, Microsoft SQL Server 2012 또는 SQL Azure)로 변경할 수 있습니다. 이렇게 하면 데이터베이스 개발을 한 프로젝트에 중앙 집중화하고 필요할 때 여러 버전의 SQL Server 인스턴스에 프로젝트를 게시할 수 있습니다.  
  
SSDT에서는 대상 플랫폼이 인식되고 코드의 오류(예를 들어 SQL Azure에 게시할 프로젝트에 지원되지 않는 기능을 사용하는 경우)가 자동으로 감지되므로 이 작업을 간단하게 수행할 수 있습니다.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 이전 절차에서 만들어진 엔터티를 활용합니다.  
  
### <a name="to-change-a-projects-target-platform"></a>프로젝트의 대상 플랫폼을 변경하려면  
  
1.  **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 왼쪽의 **프로젝트 설정** 탭을 클릭하여 **프로젝트 설정** 속성 페이지에 액세스합니다.  
  
2.  이 페이지의 **대상 플랫폼** 드롭다운 목록에는 데이터베이스 프로젝트를 게시할 수 있는 지원되는 모든 SQL Server 플랫폼이 표시됩니다. 이 절차에서는 **SQL Azure**를 선택합니다.  
  
### <a name="to-use-platform-validation-when-editing-scripts"></a>스크립트를 편집할 때 플랫폼 유효성 검사를 사용하려면  
  
1.  솔루션 탐색기에서 **Products** 테이블을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 선택하여 Transact\-SQL 편집기에서 코드를 엽니다.  
  
2.  `ON [PRIMARY]` 문의 끝에 `CREATE TABLE` 을 추가합니다.  
  
3.  **오류 목록** 창에 SQL70015: SQL Azure에서는 ‘파일 그룹 참조 및 파티션 구성표’가 지원되지 않습니다.라는 오류가 표시되는지 확인합니다.  
  
    SSDT에서는 대상 플랫폼에 따라 스크립트의 유효성을 자동으로 검사합니다. 이 예의 경우 SQL Azure에서는 파일 그룹이 지원되지 않으므로 오류가 반환됩니다. SQL Azure에서 지원되지 않는 Transact\-SQL 문 목록은 [부분적으로 지원되는 Transact-SQL 문(Microsoft Azure SQL Database)](https://msdn.microsoft.com/library/ee336267.aspx)을 참조하세요.  
  
4.  `ON` 절을 제거합니다. 오류가 즉시 **오류 목록**에서 사라집니다.  
  
### <a name="to-publish-a-database-project"></a>데이터베이스 프로젝트를 게시하려면  
  
1.  SQL Azure 인스턴스에 액세스한 경우 다음 단계로 건너뛰어도 됩니다. 그렇지 않은 경우 **솔루션 탐색기**에서 **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택하여 **프로젝트 설정** 속성 페이지에 액세스합니다. **대상 플랫폼** 드롭다운 목록을 사용하여 프로젝트를 게시할 대상 SQL Server 플랫폼을 선택합니다.  
  
2.  **솔루션 탐색기**에서 **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다. 프로젝트 빌드가 시작됩니다. 빌드 오류가 없으면 **데이터베이스 게시** 대화 상자가 나타납니다.  
  
3.  **데이터베이스 게시** 대화 상자에서 **편집** 을 클릭하여 대상 데이터베이스 연결을 편집합니다.  
  
4.  **연결 속성** 대화 상자에서 SQL Server 인스턴스 이름과 인증에 사용할 자격 증명을 입력합니다. **데이터베이스에 연결**에 **NewTrade**를 입력합니다. 이렇게 하면 데이터베이스 프로젝트가 새 데이터베이스에 게시됩니다. 기존 데이터베이스를 선택하여 여기에 게시할 수도 있습니다. 예를 들어 기존 **TradeDev** 데이터베이스를 선택한 경우 오프라인 **TradeDev** 프로젝트에서 스크립트 등의 개체에 대해 변경한 내용은 라이브 **TradeDev** 데이터베이스에 전파됩니다.  
  
    프로젝트를 게시할 대상 데이터베이스를 변경할 수 있는 권한이 있는 경우 **게시** 단추를 누릅니다. 그러나 프로덕션 데이터베이스에 대한 쓰기 권한이 없는 경우에는 **스크립트 생성** 단추를 클릭하여 Transact\-SQL 게시 스크립트를 생성한 후 이를 DBA에 전달할 수 있습니다. 그러면 DBA는 이 스크립트를 실행하여 해당 스키마가 데이터베이스 프로젝트와 동기화되도록 프로덕션 서버를 업데이트할 수 있습니다.  
  
5.  **Data Tools 작업**  창에는 게시 작업의 진행률이 표시되고 오류가 발생하는 경우 알림이 표시됩니다. 이 새 창에서 배포 미리 보기, 생성된 스크립트 또는 전체 게시 결과(원하는 경우)를 보도록 선택할 수도 있습니다.  
  
6.  이후 게시 작업에 동일한 설정을 다시 사용할 수 있도록 게시 설정을 프로필에 저장할 수도 있습니다. 이렇게 하려면 **데이터베이스 게시** 대화 상자에서 **다른 이름으로 프로필 저장** 단추를 클릭합니다. 나중에 기존 설정을 다시 로드하려면 **프로필 로드** 단추를 클릭하면 됩니다.  
  
7.  **Data Tools 작업** 창의 메시지를 확인합니다. **게시 미리 보기를 만드는 중...** 오른쪽의 "미리 보기" 링크를 클릭합니다. 그러면 배포 미리 보기 보고서가 열립니다. 프로젝트의 대상 플랫폼이 프로젝트가 게시된 데이터베이스 서버와 동일하지 않으면 SSDT는 이 보고서에 경고를 표시합니다.  예를 들어 프로젝트의 대상 플랫폼이 Microsoft SQL Server 2012인 경우 프로젝트를 SQL Server 2008 R2 서버 인스턴스에 게시하려고 하면 **출력** 창에 다음 경고가 표시됩니다.  
  
**Microsoft SQL Server 2012를 대상 플랫폼으로 지정하는 프로젝트에서 SQL Server 2008에 대한 호환성 문제가 발생할 수 있음**    Microsoft SQL Server 2012에 도입된 엔터티(예: 시퀀스 개체)가 이러한 프로젝트에 포함되어 있으면 게시 작업이 실패합니다.  
  
    The deployment will fail if object predicates use **CONTAINS** or **FREETEXT** over a newly created full-text index and transactional scripts are used. If the option to include transactional scripts is enabled during deployment, then procedures and views are defined inside a transaction while a full-text index is defined outside of a transaction at the end of the deploy script. Because of this ordering in the script, procedures or views using CONTAINS or FREETEXT will not be resolved against the full-text index, resulting in a deployment error.  
  

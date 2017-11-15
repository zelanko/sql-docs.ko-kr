---
title: "스크립트 생성 및 게시 마법사 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql9.swb.generatescriptswizard.chooseviews.f1
- sql13.swb.generatescriptswizard.manageproviders.f1
- sql9.swb.generatescriptswizard.scriptwizarddescription.f1
- sql9.swb.generatescriptswizard.choosedefaults.f1
- sql13.swb.generatescriptswizard.summarypage.f1
- sql13.swb.generatescriptswizard.providerconfiguration.f1
- sql9.swb.generatescriptswizard.chooseuddt.f1
- sql9.swb.generatescriptswizard.chooserules.f1
- sql13.swb.generatescriptswizard.introduction.f1
- sql13.swb.generatescriptswizard.setscriptingoptions.f1
- sql13.swb.generatescriptswizard.saveorpublishscripts.f1
- sql9.swb.generatescriptswizard.progress.f1
- sql9.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.welcome.f1
- sql9.swb.generatescriptswizard.scriptfileoption.f1
- sql13.swb.generatescriptswizard.chooseobjects.f1
- sql13.swb.generatescriptswizard.advancedpublishingoptions.f1
- sql9.swb.generatescriptswizard.selectdatabase.f1
- sql9.swb.generatescriptswizard.choosetables.f1
- sql9.swb.generatescriptswizard.choosestoredprocedures.f1
- sql9.swb.generatescriptswizard.chooseobjecttypes.f1
- sql13.swb.generatescriptswizard.advancedscriptingoptions.f1
- sql9.swb.generatescriptswizard.choosescriptoptions.f1
- sql9.swb.generatescriptswizard.chooseudf.f1
helpviewer_keywords:
- databases [SQL Server], publishing
- publishing databases
- scripts [SQL Server], generating
- scripts [SQL Server], publishing
- databases [SQL Server], generating scripts
- Publish Database Wizard
ms.assetid: 5ee520ba-ec7e-4199-a441-189e9e264b37
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5d10e5a92fe19da764d341039ed348f8297193a8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="generate-and-publish-scripts-wizard"></a>스크립트 생성 및 게시 마법사
  **스크립트 생성 및 게시 마법사** 를 사용하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 또는 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]인스턴스 간에 데이터베이스를 전송하는 스크립트를 만들 수 있습니다. 스크립트는 로컬 네트워크의 데이터베이스 인스턴스에 있는 데이터베이스나 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 생성할 수 있습니다. 생성된 스크립트는 데이터베이스 엔진의 다른 인스턴스나 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 실행할 수 있습니다. 마법사를 사용하여 데이터베이스 게시 서비스 프로젝트를 통해 생성된 웹 서비스에 직접 데이터베이스의 내용을 게시할 수도 있습니다. 전체 데이터베이스에 대한 스크립트를 만들거나 특정 개체로 제한할 수 있습니다.  
  
1.  **시작하기 전 주의 사항:**  [호스티드 서비스에 게시](#PubHostSvc), [사용 권한](#Permissions)  
  
2.  **스크립트를 생성하거나 게시하려면 다음을 사용합니다.**  [스크립트 생성 및 게시 마법사](#GenPubScriptWiz)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 원본 및 대상 데이터베이스는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이상을 실행하는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스에 있을 수 있습니다.  
  
###  <a name="PubHostSvc"></a> 호스티드 서비스에 게시  
 **스크립트 생성 및 게시 마법사** 는 스크립트 생성 외에도 데이터베이스를 특정 유형의 SQL Server 웹 서비스에 게시하는 데에도 사용됩니다. SQL Server Hosting Toolkit은 CodePlex의 공유 원본 프로젝트로서 데이터베이스 게시 서비스를 제공합니다. 웹 호스팅 공급자는 데이터베이스 게시 서비스 프로젝트를 사용하여 고객이 손쉽게 데이터베이스를 웹 서비스에 게시할 수 있는 웹 서비스 집합을 작성할 수 있습니다. SQL Server Hosting Toolkit을 다운로드하는 방법은 [SQL Server 데이터 게시 서비스(SQL Server Database Publishing Services)](http://go.microsoft.com/fwlink/?LinkId=142025)를 참조하세요.  
  
 데이터베이스를 웹 호스팅 서비스에 게시하려면 마법사의 **스크립팅 옵션 설정** 페이지에서 **웹 서비스에 게시** 옵션을 선택합니다.  
  
###  <a name="Permissions"></a> 사용 권한  
 데이터베이스를 게시하려면 최소한 원본 데이터베이스에 대해 db_ddladmin 고정 데이터베이스 역할의 멤버 자격이 필요하고, 호스팅 공급자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 데이터베이스 스크립트를 게시하려면 최소한 대상 데이터베이스에 대해 db_ddladmin 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
 또한 마법사를 사용하여 게시하려면 해당 호스팅 공급자 계정에 액세스하기 위한 사용자 이름과 암호를 제공해야 합니다. 원본 데이터베이스를 게시하려면 먼저 호스팅 공급자에서 대상 데이트베이스를 만들어야 합니다. 게시하면 기존 데이터베이스의 개체를 덮어씁니다.  
  
##  <a name="GenPubScriptWiz"></a> 스크립트 생성 및 게시 마법사 사용  
 **스크립트를 생성하거나 게시하려면**  
  
1.  **개체 탐색기**에서 스크립팅할 데이터베이스가 포함된 인스턴스에 대한 노드를 확장합니다.  
  
2.  **태스크**를 가리킨 다음 **스크립트 생성**을 클릭합니다.  
  
3.  마법사 대화 상자를 완료합니다.  
  
    -   [소개 페이지](#Introduction)  
  
    -   [개체 선택 페이지](#ChooseObjects)  
  
    -   [스크립팅 옵션 설정 페이지](#SetScriptOpt)  
  
    -   [고급 스크립팅 옵션 페이지](#AdvScriptOpt)  
  
    -   [공급자 관리 페이지](#MgProviders)  
  
    -   [고급 게시 옵션 페이지](#AdvPubOpts)  
  
    -   [공급자 구성 페이지](#ProvConfig)  
  
    -   [요약 페이지](#Summary)  
  
    -   [스크립트 저장 또는 게시 페이지](#SavePubScripts)  
  
###  <a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 스크립트를 생성 또는 게시하기 위한 단계에 대해 설명합니다.  
  
 **이 페이지를 다시 표시 안 함** - 다음에 **스크립트 생성 및 게시 마법사**를 시작할 때 이 페이지를 표시하지 않습니다.  
  
 **다음 >** - **방법 선택** 페이지로 진행합니다.  
  
 **취소** - 데이터베이스에서 스크립트를 생성하거나 게시하지 않고 마법사를 종료합니다.  
  
###  <a name="ChooseObjects"></a> 개체 선택 페이지  
 이 페이지를 사용하여 이 마법사에서 생성된 스크립트에 포함할 개체를 선택할 수 있습니다. 다음 마법사 페이지에서는 이러한 스크립트를 사용자가 선택한 위치에 저장하거나, 스크립트를 사용하여 데이터베이스 개체를 [SQL Server Database Publishing Services](http://go.microsoft.com/fwlink/?LinkId=142025)가 설치되어 있는 원격 웹 호스팅 공급자에 게시할 수 있습니다.  
  
 **전체 데이터베이스 스크립팅 옵션** - 데이터베이스의 모든 개체에 대한 스크립트를 생성하고 데이터베이스 자체에 대한 스크립트를 포함하려면 클릭합니다.  
  
 **특정 데이터베이스 개체 선택** - 데이터베이스에서 선택한 특정 개체에 대해서만 스크립트를 생성하도록 마법사를 제한하려면 클릭합니다.  
  
-   **데이터베이스 개체** - 스크립트에 포함할 하나 이상의 개체를 선택합니다.  
  
-   **모두 선택** - 사용 가능한 확인란을 모두 선택합니다.  
  
-   **모두 선택 취소** - 모든 확인란을 선택 취소합니다. 작업을 계속하려면 데이터베이스 개체를 적어도 하나 이상 선택해야 합니다.  
  
###  <a name="SetScriptOpt"></a> 스크립팅 옵션 설정 페이지  
 이 페이지를 사용하여 마법사에서 스크립트를 사용자가 선택한 위치에 저장할지, 아니면 스크립트를 사용하여 데이터베이스 개체를 원격 웹 호스팅 공급자에 게시할지를 지정할 수 있습니다. 게시하려면 Database Publishing Services 웹 서비스를 사용하여 설치된 웹 서비스에 액세스할 수 있어야 합니다.  
  
 **옵션** - 마법사에서 사용자가 선택한 위치에 스크립트를 저장하려면 **특정 위치에 스크립트 저장**을 선택합니다. 나중에 데이터베이스 엔진 인스턴스나 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]를 대상으로 스크립트를 실행할 수 있습니다. 데이터베이스 개체를 원격 웹 호스팅 공급자에 게시하려면 **웹 서비스에 게시**를 선택합니다.  
  
 **특정 위치에 스크립트 저장** - 하나 이상의 Transact-SQL 스크립트 파일을 지정한 위치에 저장합니다.  
  
-   **고급** - 스크립트 생성을 위한 고급 옵션을 선택할 수 있는 **고급 스크립팅 옵션** 대화 상자를 표시합니다.  
  
-   **파일에 저장** - 스크립트를 하나 이상의 .sql 파일로 저장합니다. 파일의 이름과 위치를 지정하려면 찾아보기 단추(**…**)를 클릭합니다. 이름이 같은 파일이 이미 있을 경우 해당 파일을 바꾸려면 **기존 파일 덮어쓰기** 확인란을 선택합니다. 스크립트 생성 방식을 지정하려면 **단일 파일** 또는 **개체당 단일 파일** 을 클릭합니다. 또한 스크립트에 사용할 텍스트 유형을 지정하려면 **유니코드 텍스트** 또는 **ANSI 텍스트** 를 클릭합니다.  
  
-   **클립보드에 저장** - Transact-SQL 스크립트를 클립보드에 저장합니다.  
  
-   **새 쿼리 창에 저장** - 데이터베이스 엔진 쿼리 편집기 창에 스크립트를 생성합니다. 편집기 창이 열려 있지 않으면 스크립트 대상으로 사용할 새 편집기 창이 열립니다.  
  
 **웹 서비스에 게시** - 공급자를 구성한 원격 웹 호스팅 서비스에 선택한 개체를 게시합니다.  
  
-   **공급자 관리** - **공급자 관리** 대화 상자를 표시합니다. **공급자 관리** 대화 상자를 사용하여 호스팅 공급자를 추가, 편집 및 삭제할 수 있습니다. 각 공급자는 웹 호스팅 서비스와 해당 서비스의 대상 데이터베이스에 대한 연결 정보를 지정합니다.  
  
-   **고급** - 스크립트 게시를 위한 고급 옵션을 선택할 수 있는 **고급 게시 옵션** 대화 상자를 표시합니다.  
  
-   **공급자** - 선택한 개체를 게시할 데이터베이스를 호스트하는 웹 호스팅 서비스에 대한 연결 정보를 지정하는 공급자를 선택합니다. 공급자를 선택하려면 **공급자 관리** 대화 상자에 적어도 하나 이상의 공급자가 있어야 합니다.  
  
-   **대상 데이터베이스** - 선택한 개체를 게시할 대상 데이터베이스를 선택합니다. 대상 데이터베이스를 선택하기 전에 공급자를 선택해야 합니다.  
  
###  <a name="AdvScriptOpt"></a> 고급 스크립팅 옵션 페이지  
 이 페이지를 사용하여 이 마법사에서 스크립트를 생성하는 방법을 지정할 수 있습니다. 여기에서는 다양한 옵션을 사용할 수 있습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Database engine type **에 지정된 SQL Server 또는**버전에서 지원되지 않는 옵션은 회색으로 나타납니다.  
  
 **옵션** - 각 옵션의 오른쪽에 있는 사용 가능한 설정 목록에서 값을 선택하여 고급 옵션을 지정합니다.  
  
 **일반** - 다음 옵션이 전체 스크립트에 적용됩니다.  
  
-   **ANSI 패딩** - 스크립트에 **ANSI PADDING ON** 을 포함합니다. 기본값은 **True**입니다.  
  
-   **파일에 추가** - **True**이면 **스크립팅 옵션 설정** 페이지에서 지정한 기존 스크립트의 아래쪽에 이 스크립트가 추가되고, **False**이면 새 스크립트가 이전 스크립트를 덮어씁니다. 기본값은 **False**입니다.  
  
-   **오류 발생 시 스크립팅 계속** - **True**이면 오류 발생 시 스크립팅이 중지됩니다. **False**이면 스크립팅을 계속합니다. 기본값은 **False**입니다.  
  
-   **UDDT를 기본 형식으로 변환** - **True**이면 UDDT(사용자 정의 데이터 형식)가 이 형식을 만드는 데 사용된 기본 데이터 형식으로 변환됩니다. 스크립트가 실행될 데이터베이스에 UDDT가 없으면 **True** 를 사용합니다. **False**이면 UDDT가 사용됩니다. 기본값은 **False**입니다.  
  
-   **종속 개체에 대한 스크립트 생성** - 선택한 개체의 스크립트가 실행될 때 제공되어야 할 모든 개체의 스크립트를 생성합니다. 기본값은 **True**입니다.  
  
-   **설명 머리글 포함** - **True**이면 스크립트를 각 개체별 섹션으로 구분하는 스크립트에 설명이 추가됩니다. 기본값은 **False**입니다.  
  
-   **if NOT EXISTS 포함** - **True**이면 데이터베이스에 개체가 이미 있는지 여부를 확인하는 문이 스크립트에 포함되어 개체가 있을 경우 새 개체를 만들지 않습니다. 기본값은 **False**입니다.  
  
-   **시스템 제약 조건 이름 포함** - **False**이면 원본 데이터베이스에서 자동으로 이름이 지정된 제약 조건이 대상 데이터베이스에서 자동으로 이름이 변경되고, **True**이면 제약 조건의 이름이 원본 데이터베이스와 대상 데이터베이스에서 같습니다.  
  
-   **지원되지 않는 문 포함** - **False**이면 선택된 서버 버전이나 엔진 유형에서 지원되지 않는 개체의 문은 스크립트에 포함되지 않습니다. **True**이면 스크립트에 지원되지 않는 개체가 포함됩니다. 지원되지 않는 개체의 각 문에는 선택된 SQL Server 버전이나 엔진 유형에 대해 스크립트를 실행하려면 먼저 문을 편집해야 한다는 주석이 포함됩니다. 기본값은 **False**입니다.  
  
-   **개체 이름 스키마 한정** - 만들어지는 개체 이름에 스키마 이름을 포함합니다. 기본값은 **True**입니다.  
  
-   **스크립트 바인딩** - 기본 및 규칙 개체 바인딩을 위한 스크립트를 생성합니다. 기본값은 **False**입니다. 자세한 내용은 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md) 및 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)을 참조하세요.  
  
-   **데이터 정렬 스크립팅** - 스크립트에 데이터 정렬 정보를 포함합니다. 기본값은 **False**입니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
-   **기본값 스크립팅** - 테이블 열에서 기본값을 설정하는 데 사용되는 기본 개체를 포함합니다. 기본값은 **True**입니다. 자세한 내용은 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)를 참조하세요.  
  
-   **drop 및 create 스크립팅** - **CREATE 스크립팅**이면 개체를 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 포함되고, **DROP 스크립팅**이면 개체를 삭제하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 포함됩니다. 또한 **DROP 및 CREATE 스크립팅**이면 스크립팅된 각 개체에 대해 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP 문이 스크립트에 포함되고 그 다음에 CREATE 문이 포함됩니다. 기본값은 **CREATE 스크립팅**입니다.  
  
-   **확장 속성 스크립팅** - 개체에 확장 속성이 있을 경우 스크립트에 확장 속성을 포함합니다. 기본값은 **True**입니다.  
  
-   **엔진 유형에 대한 스크립트** - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 또는 SQL Server 데이터베이스 엔진 인스턴스 중 선택된 유형에서 실행할 수 있는 스크립트를 만듭니다. 지정된 유형에 지원되지 않는 개체는 스크립트에 포함되지 않습니다. 기본값은 원본 서버의 유형입니다.  
  
-   **서버 버전에 대한 스크립트** - 선택한 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행할 수 있는 스크립트를 만듭니다. 버전의 새 기능은 이전 버전에 대해 스크립팅할 수 없습니다. 기본값은 원본 서버의 버전입니다.  
  
-   **로그인 스크립팅** - 스크립팅된 개체가 데이터베이스 사용자일 때 이 옵션을 사용하여 사용자에 대한 로그인을 만들 수 있습니다. 기본값은 **False**입니다.  
  
-   **개체 수준 사용 권한 스크립팅** - 데이터베이스의 개체에 대한 사용 권한을 설정하는 스크립트를 포함합니다. 기본값은 **False**입니다.  
  
-   **통계 스크립팅** - **통계 스크립팅**으로 설정하면 이 옵션은 개체에 대한 통계를 다시 만드는 **CREATE STATISTICS** 문을 포함합니다. **통계 및 히스토그램 스크립팅** 옵션은 히스토그램 정보도 만듭니다. 기본값은 **통계 스크립팅 안 함**입니다. 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.  
  
-   **USE DATABASE 스크립팅** - 스크립트에 **USE DATABASE** 문을 추가합니다. 올바른 데이터베이스에서 데이터베이스 개체를 만들려면 **USE DATABASE** 문을 포함해야 합니다. 다른 데이터베이스에서 스크립트가 사용되어야 할 경우에는 **False** 를 선택하여 **USE DATABASE** 문을 생략합니다. 기본값은 **True**입니다. 자세한 내용은 [USE&#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)를 참조하세요.  
  
-   **스크립팅할 데이터 형식** - 스크립팅할 항목을 선택합니다. **데이터만**, **스키마만** 또는 둘 다 선택할 수 있습니다. 기본값은 **스키마만**입니다.  
  
 **테이블/뷰 옵션** - 다음 옵션은 테이블 또는 뷰에 대한 스크립트에만 적용됩니다.  
  
-   **변경 내용 추적 스크립팅** - 원본 데이터베이스 또는 원본 데이터베이스의 테이블에서 변경 내용 추적을 사용하도록 설정되어 있는 경우 변경 내용 추적을 스크립팅합니다. 기본값은 **False**입니다. 자세한 내용은 [변경 내용 추적 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)를 참조하세요.  
  
-   **check 제약 조건 스크립팅** – **CHECK** 제약 조건을 스크립트에 추가합니다. 기본값은 **True**입니다. **CHECK** 제약 조건에서는 테이블에 입력한 데이터가 일부 지정된 조건에 맞아야 합니다. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
-   **데이터 압축 옵션 스크립팅** - 원본 데이터베이스 또는 원본 데이터베이스의 테이블에서 데이터 압축 옵션이 구성되어 있는 경우 데이터 압축 옵션을 스크립팅합니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요. 기본값은 **False**입니다.  
  
-   **외래 키 스크립팅** - 외래 키를 스크립트에 추가합니다. 기본값은 **True**입니다. 외래 키는 테이블 간의 관계를 나타내고 적용합니다.  
  
-   **전체 텍스트 인덱스 스크립팅** - 전체 텍스트 인덱스 만들기를 스크립팅합니다. 기본값은 **False**입니다.  
  
-   **인덱스 스크립팅** - 테이블에 대한 인덱스 생성을 스크립팅합니다. 기본값은 **True**입니다. 인덱스는 데이터를 신속하게 찾는 데 도움이 됩니다.  
  
-   **기본 키 스크립팅** - 테이블에 대한 기본 키 생성을 스크립팅합니다. 기본값은 **True**입니다. 기본 키는 테이블의 각 행을 고유하게 식별합니다.  
  
-   **트리거 스크립팅** - 테이블에 대한 DML 트리거 생성을 스크립팅합니다. 기본값은 **False**입니다. DML 트리거는 데이터베이스 서버에서 DML(데이터 조작 언어) 이벤트가 발생하면 실행하도록 프로그래밍된 동작입니다. 자세한 내용은 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)을 참조하세요.  
  
-   **고유 키 스크립팅** - 테이블에 대한 고유 키 생성을 스크립팅합니다. 고유 키는 중복 데이터를 입력하지 않도록 합니다. 기본값은 **True**입니다. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
###  <a name="MgProviders"></a> 공급자 관리 페이지  
 이 대화 상자를 사용하여 호스팅 공급자 연결을 보고, 추가, 편집, 삭제 또는 테스트할 수 있습니다. 호스팅 공급자는 CodePlex의 SQL Server Hosting Toolkit에 포함된 Database Publishing Service 프로젝트를 사용하여 만든 웹 서비스를 위한 연결 정보를 지정합니다.  
  
 **구성된 공급자** - 저장된 각 호스팅 공급자의 이름과 **웹** 서비스 주소를 나열합니다.  
  
 **새로 만들기** - **새 공급자의 공급자 구성** 대화 상자를 열고 새 호스팅 공급자를 추가합니다.  
  
 **편집** - 해당하는 **공급자 구성** 대화 상자를 열고 기존 호스팅 공급자를 편집합니다.  
  
 **삭제** - 선택한 호스팅 공급자를 삭제합니다.  
  
 **테스트** - 선택한 공급자의 정보를 사용하여 호스팅 서비스에 대한 연결을 테스트합니다.  
  
 **확인** - **호스팅 공급자** 대화 상자에서 변경한 내용을 모두 저장합니다.  
  
 **취소** - **호스팅 공급자** 대화 상자에서 변경한 내용을 모두 실행 취소합니다.  
  
###  <a name="AdvPubOpts"></a> 고급 게시 옵션 페이지  
 이 페이지를 사용하여 이 마법사에서 데이터베이스를 게시하는 방법을 지정할 수 있습니다. 여기에서는 다양한 옵션을 사용할 수 있습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Database engine type **에 지정된 SQL Server 또는**버전에서 지원되지 않는 옵션은 회색으로 나타납니다.  
  
 **옵션** - 각 옵션의 오른쪽에 있는 사용 가능한 설정 목록에서 값을 선택하여 고급 옵션을 지정합니다.  
  
 **일반** - 다음 옵션이 전체 게시에 적용됩니다.  
  
1.  **UDDT를 기본 형식으로 변환** - **True**이면 UDDT(사용자 정의 데이터 형식)가 이 형식을 만드는 데 사용된 기본 데이터 형식으로 변환됩니다. 스크립트가 실행될 데이터베이스에 UDDT가 없으면 **True** 를 사용합니다. **False**이면 UDDT가 사용됩니다. 기본값은 **False**입니다.  
  
2.  **데이터 정렬 게시** - 테이블 열에 대한 데이터 정렬 정보를 포함합니다. 기본값은 **False**입니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
3.  **기본값 게시** - 테이블 열에서 기본값을 설정하는 데 사용되는 기본 개체를 포함합니다. 기본값은 **True**입니다. 자세한 내용은 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)를 참조하세요.  
  
4.  **종속 개체 게시** - 선택한 개체의 스크립트가 실행될 때 제공되어야 할 모든 개체를 게시합니다. 기본값은 **True**입니다.  
  
5.  **확장 속성 게시** - 개체에 확장 속성이 있을 경우 게시하기 위해 공급자에 보내는 스크립트에 확장 속성을 포함합니다. 기본값은 **True**입니다.  
  
6.  **서버 버전에 대해 게시** - 게시하기 위해 원격 공급자에 보내는 스크립트를 선택한 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행할 수 있는 방식으로 만듭니다. 버전의 새 기능은 이전 버전에 대해 스크립팅할 수 없습니다. 기본값은 원본 서버의 버전입니다.  
  
7.  **개체 수준 사용 권한 게시** - 데이터베이스에서 선택한 개체에 대한 사용 권한을 포함합니다. 기본값은 **False**입니다.  
  
8.  **통계 게시** - **통계 게시**로 설정하면 개체에 대한 통계를 다시 만드는 **CREATE STATISTICS** 문을 포함합니다. **통계 및 히스토그램 게시** 옵션은 히스토그램 정보도 만듭니다. 기본값은 **통계 게시 안 함**입니다. 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.  
  
9. **vardecimal 옵션 게시** - **vardecimal** 테이블 형식을 원본 데이터베이스 테이블에서 사용할 수 있는 경우 대상 데이터베이스 테이블에서도 사용할 수 있도록 설정합니다. 기본값은 **True**입니다.  
  
10. **개체 이름 스키마 한정** - 만들어지는 개체 이름에 스키마 이름을 포함합니다. 기본값은 **True**입니다.  
  
11. **스크립트 바인딩** - 게시하기 위해 공급자에 보내는 스크립트에 기본 개체 및 규칙 개체에 대한 바인딩을 포함합니다. 기본값은 **True**입니다. 자세한 내용은 [CREATE DEFAULT&#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md) 및 [CREATE RULE&#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)을 참조하세요.  
  
12. **게시할 데이터 형식** - 스크립팅할 항목을 선택합니다. **데이터만**, **스키마만** 또는 둘 다 선택할 수 있습니다. 기본값은 **스키마 및 데이터**입니다.  
  
 **게시 옵션** - 웹 호스트 공급자에 게시하는 경우 트랜잭션을 사용할지 여부를 지정합니다.  
  
1.  **트랜잭션을 사용하여 게시** - 원격 웹 호스팅 공급자에 게시할 때 트랜잭션을 사용합니다. 대상 데이터베이스에서 게시를 완료할 수 없으면 트랜잭션이 롤백됩니다. 기본값은 **True**입니다.  
  
 **테이블/뷰 옵션** - 다음 옵션은 테이블 또는 뷰에만 적용됩니다.  
  
1.  **CHECK 제약 조건 게시** - 게시 프로세스에 **CHECK** 제약 조건 만들기를 포함합니다. 기본값은 **True**입니다. **CHECK** 제약 조건에서는 테이블에 입력한 데이터가 일부 지정된 조건에 맞아야 합니다. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
2.  **외래 키 게시** - 게시 프로세스에 외래 키 만들기를 포함합니다. 기본값은 **True**입니다. 외래 키는 테이블 간의 관계를 나타내고 적용합니다. 자세한 내용은 [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md)을 참조하세요.  
  
3.  **전체 텍스트 인덱스 게시** - 전체 텍스트 인덱스 만들기를 스크립팅합니다. 기본값은 **False**입니다.  
  
4.  **인덱스 게시** - 게시 프로세스에 테이블의 인덱스를 포함합니다. 기본값은 **True**입니다. 인덱스는 데이터를 신속하게 찾는 데 도움이 됩니다.  
  
5.  **기본 키 게시** - 게시 프로세스에 기본 키 만들기를 포함합니다. 기본값은 **True**입니다. 기본 키는 테이블의 각 행을 고유하게 식별합니다. 자세한 내용은 [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md)을 참조하세요.  
  
6.  **트리거 게시** - 게시 프로세스에 DML 트리거 만들기를 포함합니다. 기본값은 **True**입니다. DML 트리거는 데이터베이스 서버에서 DML(데이터 조작 언어) 이벤트가 발생하면 실행하도록 프로그래밍된 동작입니다. 자세한 내용은 [DML Triggers](../../relational-databases/triggers/dml-triggers.md)을 참조하세요.  
  
7.  **고유 키 게시** - 게시 프로세스에 테이블에 대한 고유 키 만들기를 포함합니다. 고유 키는 중복 데이터를 입력하지 않도록 합니다. 기본값은 **True**입니다. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
8.  **변경 내용 추적 게시** - 원본 데이터베이스 또는 원본 데이터베이스의 테이블에서 변경 내용 추적을 사용하도록 설정되어 있는 경우 게시 프로세스에 변경 내용 추적을 포함합니다. 기본값은 **False**입니다. 자세한 내용은 [변경 내용 추적 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)를 참조하세요.  
  
9. **데이터 압축 옵션 게시** - 원본 데이터베이스 또는 원본 데이터베이스의 테이블에서 데이터 압축 옵션이 구성되어 있는 경우 게시 프로세스에 데이터 압축 옵션을 포함합니다. 기본값은 **True**입니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
###  <a name="ProvConfig"></a> 공급자 구성 페이지  
 이 대화 상자를 사용하여 호스팅 공급자 설정을 보거나 수정할 수 있습니다. 이 대화 상자를 사용하면 다음과 같은 작업을 수행할 수 있습니다.  
  
-   호스팅 공급자에 대한 연결 정보 보기, 추가 또는 편집  
  
-   공급자 연결을 위한 데이터베이스 보기, 추가, 편집 또는 삭제  
  
-   호스팅 공급자에 대한 데이터베이스 자동 구성  
  
 호스팅 공급자는 CodePlex의 SQL Server Hosting Toolkit에 포함된 Database Publishing Service 프로젝트를 사용하여 만든 웹 서비스를 위한 연결 정보를 지정합니다.  
  
 **이름** - 호스팅 공급자의 이름입니다.  
  
 **웹 서비스 주소** - 호스팅 서비스의 HTTPS 주소입니다.  
  
 **웹 서비스 인증** - 호스팅 서비스에 로그온하는 데 필요한 사용자 이름과 암호입니다.  
  
 **암호 저장** - 로컬 컴퓨터의 암호를 암호화하고 저장합니다.  
  
 **사용 가능한 데이터베이스** - 호스팅 공급자에 대해 구성된 데이터베이스는 *server_name*.*database_name*형식으로 오름차순으로 나열됩니다.  
  
 **새로 만들기** - **데이터베이스** 구성 대화 상자를 열고 새 데이터베이스를 추가합니다.  
  
 **편집** - 선택한 데이터베이스에 대한 **데이터베이스** 구성 대화 상자를 엽니다.  
  
 **삭제** - 선택한 데이터베이스를 삭제합니다.  
  
 **기본값으로 설정** - 데이터베이스를 기본값으로 선택합니다.  
  
 **확인** - 이 대화 상자의 모든 변경 내용을 저장하고 마법사로 돌아갑니다.  
  
 **취소** - 이 대화 상자의 모든 변경 내용을 실행 취소하고 마법사로 돌아갑니다.  
  
###  <a name="Summary"></a> 요약 페이지  
 이 페이지에서는 이 마법사에서 선택한 옵션을 요약합니다. 옵션을 변경하려면 **이전**을 클릭하고, 저장하거나 게시할 스크립트 생성을 시작하려면 **다음**을 클릭합니다.  
  
 **선택 항목 검토** - 마법사의 각 페이지에서 선택한 항목을 표시합니다. 해당 페이지에서 선택한 옵션을 보려면 노드를 확장하세요.  
  
###  <a name="SavePubScripts"></a> 스크립트 저장 또는 게시 페이지  
 이 페이지를 사용하여 마법사의 진행률을 모니터링할 수 있습니다.  
  
 **자세히** - 마법사 진행률을 보려면 **동작** 열을 확인합니다. 스크립트를 생성한 후 마법사는 사용자의 선택에 따라 스크립트를 파일로 저장하거나 스크립트를 사용하여 웹 서비스에 게시합니다. 이러한 각 단계가 모두 완료되면 **결과** 열의 값을 클릭하여 해당 단계의 결과를 확인할 수 있습니다.  
  
 **보고서 저장** - 마법사의 진행률 결과를 파일로 저장하려면 클릭합니다.  
  
 **취소** - 처리가 완료되기 전이나 오류가 발생한 경우 마법사를 닫으려면 클릭합니다.  
  
 **마침** - 처리가 완료된 후에나 오류가 발생한 경우 마법사를 닫으려면 클릭합니다.  
 
## <a name="generating-scripts-on-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스에서 스크립트 생성  

"다른 이름으로 스크립팅..."을 사용할 때 구문이 생성된 경우 은 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 구문과 다르게 보이거나 오류 메시지를 받는 경우 SQL Server Management Studio의 스크립팅 옵션을 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]로 설정해야 할 수 있습니다.  

### <a name="how-to-set-default-scripting-options-to-sql-data-warehouse"></a>SQL 데이터 웨어하우스에 기본 스크립팅 옵션을 설정하는 방법  

[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 구문으로 개체를 스크립팅하려면 다음과 같이 기본 스크립팅 옵션을 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 로 설정합니다.  

1. **도구** 를 클릭한 다음 **옵션**을 클릭합니다.  
2. **일반 스크립팅 옵션** 설정에서 다음을 수행합니다.  
    1. 데이터베이스 엔진 유형에 대한 스크립트: **Microsoft Azure SQL 데이터베이스**  
    2. 데이터베이스 엔진 버전에 대한 스크립트: **Microsoft Azure SQL 데이터 웨어하우스 버전**  
3. **확인**을 클릭합니다.

### <a name="how-to-generate-scripts-for-sql-data-warehouse-when-it-is-not-the-default-scripting-option"></a>기본 스크립팅 옵션이 아닌 경우 SQL 데이터 웨어하우스에 대한 스크립트를 생성하는 방법  

위에 표시된 대로 기본 스크립팅 옵션으로 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 를 설정하면 이러한 지침은 무시될 수 있습니다. 그러나 다른 기본 스크립팅 옵션을 선택하면 오류가 발생할 수 있습니다. 오류를 방지하려면 다음 단계에 따라 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]에 대한 스크립트를 생성 및 게시합니다.  

1. SQL 데이터 웨어하우스 데이터베이스를 마우스 오른쪽 단추로 클릭합니다.  
2. **스크립트 생성...**을 선택합니다.  
3. 스크립팅하려는 개체를 선택합니다.  
4. **스크립팅 옵션**에서 **고급**을 클릭합니다. **일반** 설정에서 다음을 수행합니다.  
    1. 데이터베이스 엔진 유형에 대한 스크립트: **Microsoft Azure SQL 데이터베이스**  
    2. 데이터베이스 엔진 버전에 대한 스크립트: **Microsoft Azure SQL 데이터 웨어하우스 버전**  
5. **스크립트 저장 또는 게시** 를 클릭한 다음 **마침**을 클릭합니다.  

4단계에서 설정한 옵션은 저장되지 않습니다. 이러한 옵션을 저장하려면 **SQL 데이터 웨어하우스에 기본 스크립팅 옵션을 설정하는 방법**의 지침을 따릅니다.  
  
## <a name="see-also"></a>참고 항목  
 [SMO 설치](../../relational-databases/server-management-objects-smo/installing-smo.md)   
 [데이터베이스를 다른 서버로 복사](../../relational-databases/databases/copy-databases-to-other-servers.md)  
  
  

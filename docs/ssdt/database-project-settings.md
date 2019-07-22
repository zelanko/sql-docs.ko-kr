---
title: 데이터베이스 프로젝트 설정 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.DebugProperties
- sql.data.tools.dacsettings.dialog
- sql.data.tools.dbsqlclrlanguagevb
- SQL.DATA.TOOLS.DBADVANCEDBUILDSETTINGSCS
- sql.data.tools.dbadvancedbuildsettingscs
- ql.data.tools.criticalerror.dialog
- sql.data.tools.dbassemblysigningchangekeypassword
- sql.data.tools.advanceddeploymentsystemdefined.dialog
- sql.data.tools.advanceddatabasesettings.dialog
- sql.data.tools.extendedpropertiesvalueeditor.dialog
- sql.data.tools.dbsqlclrlanguagecs
- ql.data.tools.dbassemblysigningpasswordneeded
- sql.data.tools.vbadvancedsettings.dialog
- sql.data.tools.dbsqlclr
- sql.data.tools.SqlCmdVariablesProperties
- sql.data.tools.dbassemblysigning
- sql.data.tools.advanceddeploymentsettings.dialog
- sql.data.tools.advancedpublishsettings.dialog
- sql.data.tools.BuildActionProperties
- sql.data.tools.serverselectionpolicy.dialog
- sql.data.tools.dbadvancedbuildsettingsvb
- sql.data.tools.dbprojectwizard.buildeventcommandline
- sql.data.tools.dbreferencepaths
- sql.data.tools.GeneralProperties
- sql.data.tools.BuildProperties
- sql.data.tools.DeployProperties
- sql.data.tools.csadvancedsettings.dialog
- sql.data.tools.dbassemblyinfo
- sql.data.tools.extendedpropertieseditor.dialog
ms.assetid: 34418730-1aaa-4948-aee2-8f1e62cda85c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4921df6e1602d4cfc98aa6da3733452d6b5d33d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912849"
---
# <a name="database-project-settings"></a>데이터베이스 프로젝트 설정
데이터베이스 프로젝트 설정을 사용하여 데이터베이스, 디버깅 및 빌드 구성의 여러 측면을 제어할 수 있습니다. 이러한 설정은 다음 범주로 구분됩니다.  
  
-   [프로젝트 설정](#bkmk_proj_settings)  
  
-   [확장 Transact-SQL 확인](#bkmk_evf)  
  
-   [SQLCLR](#bkmk_sqlclr)  
  
-   [SQLCLR 및 SQLCLR 빌드](#bkmk_sqlclr_sqlclrbuild)  
  
-   [빌드](#bkmk_build)  
  
-   [SQLCMD 변수](#bkmk_sqlcmd_variables)  
  
-   [빌드 이벤트](#bkmk_build_events)  
  
-   [디버그](#bkmk_debug)  
  
-   [참조 경로](#bkmk_ref_paths)  
  
-   [코드 분석](#bkmk_code_analysis)  
  
### <a name="to-configure-properties-for-your-database-project"></a>데이터베이스 프로젝트에 대한 속성을 구성하려면  
  
1.  **솔루션 탐색기**에서 속성을 구성할 데이터베이스 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
    또는 **솔루션 탐색기** 에서 프로젝트의 **속성**노드를 두 번 클릭합니다.  
  
2.  데이터베이스 프로젝트에 대한 속성 시트가 나타납니다.  
  
3.  **프로젝트 설정** 탭을 클릭합니다. 이제 데이터베이스 프로젝트 속성의 일반 속성을 구성할 수 있습니다. 왼쪽 창에서는 각기 다른 범주를 나타내는 다양한 탭을 사용할 수 있습니다.  
  
## <a name="bkmk_proj_settings"></a>프로젝트 설정  
다음 표의 설정은 이 데이터베이스 프로젝트의 모든 구성에 적용됩니다.  
  
|필드|기본값|설명|  
|---------|-----------------|---------------|  
|대상 플랫폼|Microsoft SQL Server 2012|이 데이터베이스 프로젝트에서 대상으로 하는 SQL Server의 버전을 지정합니다.|  
|일반 개체에 대한 확장 Transact\-SQL 확인을 사용하도록 설정합니다.|이 옵션은 새 프로젝트를 만들 때 사용하지 않도록 설정됩니다.<br /><br />이 옵션은 SQL Azure에 연결된 SQL Server 개체 탐색기에서 프로젝트를 만들 때 또는 SQL Azure 데이터베이스를 프로젝트에 가져올 때 또는 프로젝트의 대상 플랫폼을 SQL Azure로 변경할 때 사용하도록 설정됩니다.|이 옵션을 사용하도록 설정되어 있으면 프로젝트에서 실패한 SQL Server 컴파일러 확인이 발견되었다는 오류가 보고됩니다. 대상 플랫폼을 SQL Azure로 변경하면 확장 확인을 사용하도록 설정됩니다. 대상 플랫폼을 변경해도 이 옵션의 선택은 취소되지 않습니다.<br /><br />SQL Server의 다른 버전에 대해서는 이 옵션을 사용하도록 설정할 수 있지만 유효성 검사는 Microsoft SQL Server 2012가 부분적으로 포함된 데이터베이스 및 SQL Azure로 제한됩니다. 모든 SQL Server 버전에서 모든 Transact\-SQL 구문을 지원하는 것은 아닙니다.<br /><br />자세한 내용은 이 항목의 뒷부분에 나오는 [확장 Transact-SQL 확인](#bkmk_evf)을 참조하세요.|  
|출력 형식|||  
|데이터 계층 응용 프로그램(.dacpac 파일)|활성화되고 잠겨 있습니다. 데이터베이스 프로젝트의 빌드 출력은 항상 프로젝트를 빌드할 때 .dacpac 패키지를 생성합니다.|“하위 수준 .dacpac 파일(v2.0) 추가로 만들기” 옵션이 있는 SSDT(SQL Server Data Tools) 버전을 사용하는 경우 패키지가 SQL Server Management Studio 또는 SQL Azure Management 포털과 호환되도록 할 것인지 확인합니다. (SSDT)에서 직접 .dacpac 패키지를 배포할 수 있지만 SQL Server Data Tools가 릴리스된 때 SQL Server Management Studio를 통해 버전 2.0 .dacpac 파일만 배포할 수 있습니다.|  
|스크립트 만들기(.sql 파일)||전체 .sql CREATE 스크립트가 프로젝트의 모든 개체에 대해 생성되어 프로젝트가 빌드될 때 bin\debug 폴더에 배치되는지 여부를 지정합니다 **프로젝트 게시** 명령 또는 SQL Compare 유틸리티를 사용하여 증분 업데이트 스크립트를 만들 수 있습니다.|  
|제네릭|||  
|기본 스키마|dbo|SQLCLR 및 Transact\-SQL 개체가 만들어지는 기본 스키마를 지정합니다. 개체에 스키마를 직접 지정하여 이 설정을 재정의할 수 있습니다.”|  
|파일 이름에 스키마 이름 포함|아니요|파일 이름에 스키마를 접두사로 포함할지 여부를 지정합니다(예: dbo.Products.table.sql). 이 확인란의 선택을 취소하면 개체의 파일 이름이 ObjectName.ObjectType.sql(예: Products.table.sql) 형식을 사용합니다.|  
|식별자의 대/소문자 확인|예|프로젝트를 빌드할 때 프로젝트의 SQL 개체에서 식별자의 대/소문자가 확인되는지 여부를 지정합니다. 이 옵션은 데이터베이스에 대해 대/소문자 구분 데이터 정렬을 지정하는 데이터베이스 프로젝트에 적용됩니다.|  
|데이터베이스 설정|데이터베이스에 대한 표준 구성 설정을 기반으로 하는 기본 설정|지정할 수 있는 설정의 예는 SQL Server 데이터베이스에 대한 데이터 정렬 메서드 및 데이터베이스 수준을 포함합니다.|  
  
## <a name="bkmk_evf"></a>확장 Transact-SQL 확인  
  
> [!IMPORTANT]  
> 확장 Transact-SQL 확인 기능은 SQL Server Data Tools의 다음 기능 릴리스와 Visual Studio의 다음 주요 릴리스에서 제거됩니다.  
  
확장 Transact-SQL 확인은 개발자가 빌드할 때 데이터베이스 프로젝트를 Transact-SQL 컴파일러 서비스에 전송하여 SQL Server 엔진의 파서 및 인터프리터에 대한 해당 코드의 유효성을 검사할 수 있도록 하는 데이터베이스 프로젝트 시스템에 있는 기능입니다.  
  
### <a name="transact-sql-compiler-service"></a>Transact-SQL 컴파일러 서비스  
Transact-SQL 컴파일러 서비스는 Microsoft SQL Server 2012 데이터베이스 엔진 기반의 구성 요소입니다. 이 서비스는 Microsoft SQL Server 2012 데이터베이스 엔진의 정확성과 동일한 수준으로 DDL 문의 구문 및 의미 체계의 유효성을 검사합니다. 이는 기본적으로 컴파일러 서비스가 Microsoft SQL Server 2012에서 더 이상 사용되지 않은 구문 또는 기능을 지원하지 않음을 의미합니다. 더 이상 사용되지 않는 기능에 대한 자세한 내용은 [SQL Server 2012에서 지원되지 않는 데이터베이스 엔진 기능](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)을 참조하세요.  
  
데이터베이스 프로젝트의 유효성 검사 목적으로 컴파일러 서비스는 부분적으로 포함된 데이터베이스를 만들고 해당 데이터베이스에 대한 DDL 문의 실행을 시뮬레이션합니다. 자세한 내용은 [부분적으로 포함된 데이터베이스](https://msdn.microsoft.com/library/ff929071%28v=SQL.110%29.aspx)를 참조하십시오.  
  
컴파일러 서비스에는 두 가지 범주의 제한이 있습니다.  
  
데이터베이스 또는 인스턴스 구성에 의존하는 기능(다음 항목 포함)  
  
-   세 부분 또는 네 부분 개체 참조  
  
-   FileTable  
  
-   변경 내용 추적  
  
-   Rowset 함수 - OPENROWSET, OPENQUERY, OPENDATASOURCE  
  
-   전체 텍스트 의미 체계 검색  
  
현재 유효성 검사에 지원되지 않는 기능(다음 항목 포함)  
  
-   Service Broker  
  
-   사용자 정의 파일 그룹이 포함된 분할된 스키마  
  
-   SQL Azure 메타데이터 데이터 정렬(컴파일러 서비스는 SQL Server 2012 부분적으로 포함된 데이터베이스 메타데이터 데이터 정렬 - Latin1_General_100_CI_AS_KS_WS_SC를 사용함)  
  
### <a name="enablingdisabling-extended-verification"></a>확장 확인 설정/해제  
확장 Transact-SQL 확인은 기본적으로 해당 대상 플랫폼이 SQL Azure로 설정된 SQL Azure 데이터베이스 또는 프로젝트에서 직접 만든 데이터베이스 프로젝트에서 사용하도록 설정됩니다. SQL Azure 또는 SQL Server 2012를 대상으로 하는 응용 프로그램 범위의 데이터베이스를 개발할 때 확장 확인을 사용하는 것이 좋습니다. 애플리케이션 범위의 데이터베이스에 대한 자세한 내용은 [부분적으로 포함된 데이터베이스](https://msdn.microsoft.com/library/ff929071%28v=SQL.110%29.aspx)를 참조하십시오.  
  
확장 확인은 Microsoft SQL Server 2012 및 SQL Azure와의 호환성을 얻을 수 있도록 SQL Server 2008/R2용 애플리케이션 범위의 데이터베이스를 개발할 때에도 사용할 수 있습니다.  
  
##### <a name="to-enable-or-disable-extended-verification-at-the-project-level"></a>프로젝트 수준에서 확장 확인을 설정하거나 해제하려면  
  
1.  **솔루션 탐색기**에서 프로젝트 파일을 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
2.  **프로젝트 설정**의 **대상 플랫폼**에서 **일반 개체에 대한 확장 Transact-SQL 확인을 사용하도록 설정**을 선택하거나 선택을 취소합니다.  
  
##### <a name="to-disable-extended-verification-at-the-file-level"></a>파일 수준에서 확장 확인을 해제하려면  
  
1.  **솔루션 탐색기**에서 .sql 파일을 마우스 오른쪽 단추로 두 번 클릭합니다.  
  
    > [!NOTE]  
    > 파일 수준에서 확장 Transact\-SQL 확인 기능을 사용하지 않으려면 **빌드 작업** 속성을 **빌드**로 설정해야 합니다.  
  
2.  **속성**에서 **확장 T-SQL 확인** 속성을 **False**로 변경합니다.  
  
![파일 속성](../ssdt/media/ssdt-evf.gif "파일 속성")  
  
### <a name="special-considerations-for-collations"></a>데이터 정렬에 대한 특별 고려 사항  
부분적으로 포함된 데이터베이스의 데이터 정렬에 대한 자세한 내용은 [포함된 데이터베이스 데이터 정렬](https://msdn.microsoft.com/library/ff929080%28v=sql.110%29.aspx)을 참조하십시오.  
  
## <a name="bkmk_sqlclr"></a>SQLCLR  
어셈블리 옵션에 대한 자세한 내용은 [어셈블리 정보 대화 상자](https://msdn.microsoft.com/library/1h52t681.aspx?queryresult=true)를 참조하십시오.  
  
서명에 대한 자세한 내용은 **서명 페이지, 프로젝트 디자이너** 항목의 [어셈블리 서명](https://msdn.microsoft.com/library/0k50fs3b.aspx?queryresult=true) 섹션을 참조하십시오.  
  
## <a name="bkmk_sqlclr_sqlclrbuild"></a>SQLCLR 및 SQLCLR 빌드  
**SQLCLR** 및 **SQLCLR 빌드** 속성 페이지에는 프로젝트에서 SQL CLR 개체를 사용하기 위한 여러 설정이 포함되어 있습니다. 특히 **SQLCLR** 속성 페이지에는 SQLCLR 어셈블리에 대한 사용 권한을 설정할 수 있는 권한 수준 설정이 있습니다. 또한 이 페이지에는 프로젝트에 추가된 SQLCLR 개체에 대한 DDL(Dynamic Data Language)을 생성할지 여부를 제어하는 “DDL 생성” 설정도 있습니다. SQLCLR **빌드** 속성 페이지에는 프로젝트에서 SQLCLR 코드의 컴파일을 구성하기 위해 설정할 수 있는 모든 컴파일러 옵션이 포함되어 있습니다.  
  
**SQLCLR 빌드** 속성 페이지에는 SQL CLR 개체 빌드를 위한 고급 빌드 설정이 포함되어 있습니다. SQL CLR 개체를 코딩하는 데 사용한 언어(VB 또는 C#)를 기반으로 각기 다른 옵션이 제공됩니다.  
  
1.  C#를 사용하여 개체를 작성한 경우 **SQLCLR 빌드** 속성 페이지의 **고급** 단추를 클릭하여 옵션을 사용할 수 있습니다. C# 옵션에 대한 설명은 [고급 빌드 설정 대화 상자(C#)](https://msdn.microsoft.com/library/s4wcexbc.aspx)를 참조하세요.  
  
2.  VB를 사용하여 개체를 작성한 경우 먼저 **언어** 드롭다운 목록에서 VB를 선택한 다음 **고급** 버튼을 클릭하십시오. VB 옵션에 대한 설명은 [고급 컴파일러 설정 대화 상자(Visual Basic)](https://msdn.microsoft.com/library/07bysfz2.aspx)를 참조하세요.  
  

## <a name="bkmk_build"></a>빌드  
솔루션의 각 데이터베이스 프로젝트에 대한 빌드 구성을 선택할 수 있습니다. 기본적으로 하나의 구성이 있지만 사용자 지정 구성을 추가할 수 있습니다. 예를 들어, 언제든지 데이터베이스를 삭제한 후 다시 생성할 수 있는 사용자 지정 구성을 원한다면 추가할 수 있습니다. 각기 다른 프로젝트 형식을 포함하고 있는 솔루션에서는 각 프로젝트를 위한 특정 빌드 구성을 포함한 사용자 지정 솔루션 구성을 만들 수 있습니다.  
  
#### <a name="to-specify-a-build-configuration-for-a-solution"></a>솔루션에 대한 빌드 구성을 지정하려면  
  
1.  **솔루션 탐색기**에서 빌드 구성을 지정할 솔루션 노드를 클릭합니다.  
  
2.  **빌드** 메뉴에서 **구성 관리자**를 클릭합니다. **구성 관리자** 대화 상자가 나타납니다.  
  
    솔루션의 각 프로젝트에 사용할 구성 설정을 지정합니다.  
  
#### <a name="to-specify-a-build-configuration-for-a-database-project"></a>데이터베이스 프로젝트에 대한 빌드 구성을 지정하려면  
  
1.  **솔루션 탐색기**에서 빌드 구성을 지정할 데이터베이스 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **빌드** 탭에서 **구성** 드롭다운 목록을 사용하여 이 프로젝트에 사용할 구성 설정을 지정합니다.  
  
다음 표의 설정은 이 데이터베이스 프로젝트의 모든 빌드 구성에 적용됩니다.  
  
|필드|기본값|설명|  
|---------|-----------------|---------------|  
|빌드 출력 경로|bin\Debug\|데이터베이스 프로젝트를 빌드하거나 배포할 때 빌드 출력이 생성될 위치를 지정합니다. 상대 경로를 지정하는 경우에는 데이터베이스 프로젝트 경로에 상대적인 경로를 지정해야 합니다. 경로가 없으면 새로 만들어집니다.|  
|빌드 출력 파일 이름|*DatabaseProjectName*|데이터베이스 프로젝트를 빌드할 때 생성되는 출력에 부여할 이름을 지정합니다.|  
|Transact\-SQL 경고를 오류로 처리|아니오|Transact\-SQL 경고 발생 시 빌드 및 배포 프로세스를 취소해야 하는지 여부를 지정합니다. 이 확인란의 선택을 취소하는 경우 경고가 나타나지만 빌드 및 배포 프로세스가 계속됩니다. 이 설정은 사용자가 아니라 프로젝트와 관련이 있으며 .sqlproj 파일에 저장됩니다.|  
|Transact\-SQL 경고 표시 안 함|비어 있음|표시하지 않을 경고를 식별하는 번호를 쉼표나 세미콜론으로 구분된 경고 목록으로 지정합니다.<br /><br />표시하지 않을 경고는 **Transact\-SQL 경고를 오류로 처리** 확인란을 선택해도 **오류 목록** 창에 나타나지 않으며 빌드에도 영향을 주지 않습니다.|  
  
## <a name="bkmk_sqlcmd_variables"></a>SQLCMD 변수  
SQL Server 데이터베이스 프로젝트에서 SQLCMD 변수를 사용하여 디버깅 또는 게시에 사용할 동적 대체를 제공할 수 있습니다. 빌드하는 동안 변수 이름과 값을 입력하면 값이 대체됩니다. 로컬 값이 없는 경우에는 기본값이 사용됩니다. 프로젝트 속성에 이러한 변수를 입력함으로써 게시에 자동으로 제공되며 게시 프로필에 저장됩니다. 값 로드 단추를 통해 변수의 프로젝트 값을 게시로 가져올 수 있습니다.  
  
이러한 변수는 프로젝트의 스크립트에 대해 유효성을 검사하지 않거나 자동으로 채워진 스크립트에 사용되는 변수가 아니므로 프로젝트 속성에 올바른 변수를 입력해야 합니다.  
  
또한 명령줄 게시를 사용하면 명령줄 또는 프로필을 사용하여 이 값을 재정의할 수 있습니다.  
  
## <a name="bkmk_build_events"></a>빌드 이벤트  
이 설정을 사용하여 빌드 작업이 시작되기 전에 실행할 명령줄과 빌드 작업이 완료된 후 실행할 명령줄을 지정할 수 있습니다.  
  
|필드|기본값|설명|  
|---------|-----------------|---------------|  
|빌드 전 이벤트 명령줄|없음|프로젝트가 빌드되기 전에 실행할 명령줄을 지정합니다. **빌드 전 편집**을 클릭하여 명령줄을 수정합니다.|  
|빌드 후 이벤트 명령줄|없음|프로젝트가 빌드된 후에 실행할 명령줄을 지정합니다. **빌드 후 편집**을 클릭하여 명령줄을 수정합니다.|  
|빌드 후 이벤트 실행|빌드가 성공한 경우|빌드 후 명령줄이 항상 실행되어야 하는지, 빌드 작업이 성공한 경우에만 실행되어야 하는지, 아니면 빌드 작업에서 프로젝트 출력(빌드 스크립트)을 업데이트한 경우에만 실행되어야 하는지를 지정합니다.|  
  
## <a name="bkmk_debug"></a>디버그  
이러한 설정을 사용하여 데이터베이스 프로젝트의 디버깅을 제어할 수 있습니다.  
  
|필드|기본값|설명|  
|---------|-----------------|---------------|  
|작업을 시작합니다.|없음|프로젝트를 디버그할 때 실행할 스크립트 또는 외부 프로그램을 지정합니다.|  
|대상 연결 문자열|Data Source=(localdb)\\*SolutionName*;Initial Catalog=*DatabaseProjectName*;Integrated Security=True;Pooling=False;Connect Timeout=30|지정한 빌드 구성에 대해 대상으로 할 데이터베이스 서버의 연결 정보를 지정합니다. 기본 연결 문자열은 동적으로 만들어진 SQL Server LocalDB 인스턴스 및 데이터베이스에 대한 것입니다.|  
|데이터베이스 속성 배포|예|데이터베이스 프로젝트를 배포할 때 DatabaseProerties.DatabaseProperties 설정을 배포 또는 업데이트할지 여부를 지정합니다.|  
|항상 데이터베이스 다시 만들기|아니오|증분 업데이트를 수행하는 대신 데이터베이스를 삭제하고 다시 만들지 여부를 지정합니다. 예를 들어 데이터베이스 전체 배포에 대해 데이터베이스 단위 테스트를 실행하려는 경우에 이 확인란을 선택할 수 있습니다. 이 확인란의 선택을 취소하면 기존 데이터베이스가 삭제된 다음 다시 생성되지 않고 업데이트됩니다.|  
|데이터가 손실되면 증분 배포 차단|예|업데이트로 인해 데이터가 손실될 경우 배포 작업을 중지할지 여부를 지정합니다. 이 확인란을 선택하면 데이터 손실을 초래하는 변경 내용이 있을 경우 오류가 발생하며 배포가 중지되므로 데이터가 손실되지 않습니다. 예를 들어 `varchar(50)` 열을 `varchar(30)`으로 변경할 경우 배포가 중지됩니다.<br /><br />**참고:** 데이터가 손실될 수 있는 테이블에 데이터가 들어 있는 경우에만 배포가 차단됩니다. 손실될 데이터가 없는 경우에는 배포가 계속됩니다.|  
|프로젝트가 아니라 대상에 있는 DROP 개체|아니오|데이터베이스 프로젝트에 없지만 대상 데이터베이스에 있는 개체를 배포 스크립트의 일부로 삭제해야 하는지 여부를 지정합니다. 프로젝트의 일부 파일을 제외하여 빌드 스크립트에서 일시적으로 제거할 수 있습니다. 그러나 해당 개체의 기존 버전은 대상 데이터베이스에 유지할 수 있습니다. **항상 데이터베이스 다시 만들기** 확인란을 선택한 경우에는 데이터베이스가 삭제되므로 이 확인란이 아무런 영향을 주지 않습니다.|  
|ALTER ASSEMBLY 문을 사용하여 CLR 형식 업데이트 안 함|아니오|변경 내용을 배포할 때 ALTER ASSEMBLY 문을 사용하여 CLR(공용 언어 런타임) 형식을 업데이트할지, 아니면 CLR 형식을 인스턴스화하는 개체를 삭제한 다음 다시 만들지를 지정합니다.|  
|고급...|아니오|배포를 위한 이벤트와 동작을 제어하는 옵션을 지정할 수 있는 명령 단추입니다.|  
  
## <a name="bkmk_ref_paths"></a>참조 경로  
이 페이지를 사용하여 서버를 정의하고 크로스 데이터베이스 참조에 관련된 데이터베이스 변수를 정의할 수 있습니다. 또한 해당 변수의 값을 지정할 수 있습니다. 자세한 내용은 [데이터베이스 프로젝트에서 참조 사용](https://msdn.microsoft.com/library/bb386242.aspx)을 참조하세요.  
  
## <a name="bkmk_code_analysis"></a>코드 분석  
코드 분석을 사용하여 디자인, 명명 및 성능 문제와 같은 스크립트의 잠재적 문제를 찾을 수 있습니다. 데이터베이스 프로젝트에 대한 규칙은 특정 영역을 대상으로 하는 미리 정의된 규칙 집합으로 구성되어 있으며, **프로젝트 속성** 페이지의 **코드 분석** 탭에서 규칙을 사용하거나 사용하지 않도록 설정할 수 있습니다. 동일한 탭에서 프로젝트가 빌드될 때마다 코드 분석이 자동으로 실행되도록 지정하거나, 경고를 오류로 처리할지 여부를 지정할 수 있습니다.  
  
코드 분석을 수동으로 사용하려면 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **코드 분석 실행**을 선택합니다. 코드 분석 경고는 **오류 목록** 창에 표시됩니다. 경고를 두 번 클릭하여 문제가 포함된 원본 코드로 이동하고 **오류 도움말 표시** 상황에 맞는 메뉴를 사용하여 경고에 대한 추가 정보와 가능한 해결 방법을 볼 수 있습니다. 코드 분석에 대한 자세한 내용은 [데이터베이스 코드를 분석하여 코드 품질 향상](https://msdn.microsoft.com/library/dd172133.aspx)을 참조하세요.  
  

---
title: dbSqlPackage 공급자와 함께 MSDeploy 사용 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 213b91ab-03e9-431a-80f0-17eed8335abe
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db2861b82adfa29fc0141a326b0c54b4d0ff09aa
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094907"
---
# <a name="using-msdeploy-with-dbsqlpackage-provider"></a>dbSqlPackage 공급자와 함께 MSDeploy 사용
**DbSqlPackage**는 SQL Server/SQL Azure 데이터베이스와 상호 작용할 수 있는 **MSDeploy** 공급자입니다. **DbSqlPackage**에서는 다음 작업을 지원합니다.  
  
-   **Extract**: 라이브 SQL Server 또는 SQL Azure 데이터베이스에서 데이터베이스 스냅숏(.dacpac) 파일을 만듭니다.  
  
-   **Publish**: 원본 .dacpac 파일의 스키마와 일치하도록 데이터베이스 스키마를 증분식으로 업데이트합니다.  
  
-   **DeployReport**: 게시 작업으로 변경된 사항의 XML 보고서를 만듭니다.  
  
-   **Script**: 게시 작업에서 실행하는 스크립트와 같은 Transact\-SQL 스크립트를 만듭니다.  
  
DACFx에 대한 자세한 내용은 [http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.aspx](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.aspx)의 DACFx 관리되는 API 설명서 또는 [SqlPackage.exe](../tools/sqlpackage.md)(DACFx 명령줄 도구)를 참조하세요.  
  
> [!IMPORTANT]  
> dbSqlPackage 공급자 기능은 Visual Studio의 다음 주요 릴리스에서 제거됩니다. 웹 배포를 사용하여 데이터베이스 게시를 수행하는 방법에 대한 자세한 내용은 [증분 데이터베이스 게시를 위한 dbDacFx 공급자](http://www.iis.net/learn/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing)를 참조하세요.  
  
## <a name="command-line-syntax"></a>명령줄 구문  
**dbSqlPackage** 공급자를 사용하는 **MSDeploy**는 다음 형식의 명령줄을 사용합니다.  
  
```  
  
MSDeploy –verb: MSDeploy-verb –source:dbSqlPackage="Input"[,dbSqlPackage-source-parameters] –dest:dpSqlPackage="Input"[,dbSqlPackage-target-parameters]  
```  
  
## <a name="ms-deploy-verbs"></a>MS-Deploy 동사  
**–verb** 스위치를 사용하여 MS-Deploy 명령줄에 MS-Deploy 동사를 지정합니다. **dbSqlPackage** 공급자는 다음 **MSDeploy** 동사를 지원합니다.  
  
|동사|설명|  
|--------|---------------|  
|덤프(dump)|.dacpac 파일에 포함된 원본 데이터베이스에 대한 이름, 버전 번호 및 설명 등의 정보를 제공합니다. 명령줄에 다음 형식을 사용하여 원본 데이터베이스를 지정합니다.<br /><br />**msdeploy –verb:dump –source:dbSqlPackage=”***.dacpac-file-path***”**|  
|동기화|명령줄에 다음 형식을 사용하여 dbSqlPackage 작업을 지정합니다.<br /><br />**msdeploy –verb:sync –source:dbSqlPackage**=”input” *[,DbSqlPackage-source-parameters] -***dest:dbSqlPackage**=”input” *[,DbSqlPackage-destination-parameters]*<br /><br />동기화 동사의 올바른 원본 및 대상 매개 변수는 아래 단원을 참조하십시오.|  
  
## <a name="dbsqlpackage-source"></a>dbSqlPackage 원본  
**dbSqlPackage** 공급자는 유효한 SQL Server 또는 SQL Azure 연결 문자열 또는 디스크의 .dacpac 파일에 대한 경로인 입력을 받아들입니다.  공급자의 입력 원본을 지정하는 구문은 다음과 같습니다.  
  
|Input|Default|설명|  
|---------|-----------|---------------|  
|**-source:dbSqlPackage=**{*input*}|**해당 사항 없음**|*input*은 유효한 SQL Server 또는 SQL Azure 연결 문자열 또는 디스크의 .dacpac 파일에 대한 경로입니다.<br /><br />**참고:** 연결 문자열을 입력 원본으로 사용할 때 지원되는 연결 문자열 속성은 *InitialCatalog, DataSource, UserID, Password, IntegratedSecurity, Encrypt, TrustServerCertificate* 및 *ConnectionTimeout*뿐입니다.|  
  
입력 원본이 라이브 SQL Server/SQL Azure 데이터베이스에 대한 연결 문자열인 경우 **dbSqlPackage** 라이브 SQL Server/SQL Azure 데이터베이스에서 데이터베이스 스냅숏(.dacpac 파일 형식)을 추출합니다.  
  
**원본** 매개 변수는 다음과 같습니다.  
  
|매개 변수|Default|설명|  
|-------------|-----------|---------------|  
|**Profile**:{ *string*}|해당 사항 없음|DAC 게시 프로필에 대한 파일 경로를 지정합니다. 프로필은 결과 dacpac를 생성할 때 사용할 속성 및 변수 컬렉션을 정의합니다. 게시 프로필은 대상에 전달되고 **Publish**, **Script** 또는 **DeployReport** 작업 중 하나를 수행할 때 기본 옵션으로 사용됩니다.|  
|**DacApplicationName**={ *string* }|데이터베이스 이름|DACPAC 메타데이터에 저장할 응용 프로그램 이름을 정의합니다. 기본 문자열은 데이터베이스 이름입니다.|  
|**DacMajorVersion** ={*integer*}|**1**|DACPAC 메타데이터에 저장할 주 버전을 정의합니다.|  
|**DacMinorVersion**={*integer*}|**0**|DACPAC 메타데이터에 저장할 부 버전을 정의합니다.|  
|**DacApplicationDescription**={ *string* }|해당 사항 없음|DACPAC 메타데이터에 저장할 응용 프로그램 설명을 정의합니다.|  
|**ExtractApplicationScopedObjectsOnly={True &#124; False}**|**True**|**True**인 경우 원본에서 응용 프로그램 범위의 개체만 추출합니다. **False**인 경우 응용 프로그램 범위의 개체 및 응용 프로그램 범위 밖의 개체를 모두 추출합니다.|  
|**ExtractReferencedServerScopedElements={True &#124; False}**|**True**|**True**인 경우 원본 데이터베이스 개체에서 참조하는 로그인, 서버 감사 및 자격 증명 개체를 추출합니다.|  
|**ExtractIgnorePermissions={True &#124; False}**|**False**|**True**인 경우 추출된 모든 개체에서 추출 권한을 무시하며, **False**인 경우는 그렇지 않습니다.|  
|**ExtractStorage={File&#124;Memory}**|**최근에 사용한 파일**|추출 중에 사용되는 스키마 모델에 대한 지원 저장소 유형을 지정합니다.|  
|**ExtractIgnoreExtendedProperties={True&#124;False}**|**False**|확장된 속성을 무시할지 여부를 지정합니다.|  
|**VerifyExtraction = {True&#124;False}**|**False**|추출된 dacpac를 확인할지 여부를 지정합니다.|  
  
## <a name="dbsqlpackage-destination"></a>DbSqlPackage 대상  
**dbSqlPackage** 공급자는 유효한 SQL Server/SQL Azure 연결 문자열 또는 디스크의 .dacpac 파일에 대한 경로를 대상 입력으로 받아들입니다.  공급자의 대상을 지정하는 구문은 다음과 같습니다.  
  
|Input|Default|설명|  
|---------|-----------|---------------|  
|-**dest:dbSqlPackage**={*input*}|해당 사항 없음|*input*은 유효한 SQL Server 또는 SQL Azure 연결 문자열 또는 디스크의 .dacpac 파일에 대한 전체 또는 부분 경로입니다. *input*이 파일 경로인 경우 다른 명명된 매개 변수는 지정할 수 없습니다.|  
  
모든 **dbSqlPackage** 작업에 다음 **대상** 매개 변수를 사용할 수 있습니다.  
  
|속성|Default|설명|  
|------------|-----------|---------------|  
|**Action={Publish&#124;DeployReport&#124;Script}**|해당 사항 없음|**대상**에서 수행할 작업을 지정하는 선택적 매개 변수입니다.|  
|**AllowDropBlockingAssemblies ={True &#124; False}**|**False**|**SqlClr** 게시에서 배포 계획의 일부로 차단 어셈블리를 삭제할지 여부를 지정합니다. 기본적으로, 어셈블리를 삭제해야 하는 경우에는 모든 차단 또는 참조 어셈블리가 어셈블리 업데이트를 차단합니다.|  
|**AllowIncompatiblePlatform={True &#124; False}**|**False**|SQL Server 플랫폼이 호환되지 않을 수 있는 경우에도 게시 작업을 진행해야 하는지 여부를 지정합니다.|  
|**BackupDatabaseBeforeChanges={True &#124; False}**|**False**|변경 내용을 배포하기 전 데이터베이스를 백업합니다.|  
|**BlockOnPossibleDataLoss={ True &#124; False}**|**True**|게시 작업으로 인해 데이터 손실이 발생할 수 있는 경우 게시 에피소드를 종료할지 여부를 지정합니다.|  
|**BlockWhenDriftDetected={ True &#124; False}**|**True**|스키마가 더 이상 해당 등록과 일치하지 않거나 등록이 해제된 데이터베이스 업데이트를 차단할지 여부를 지정합니다.|  
|**CommentOutSetVarDeclarations= {True &#124; False}**|**False**|생성된 게시 스크립트에서 **SETVAR** 변수 선언을 주석 처리할지 여부를 지정합니다. 게시할 때 **SQLCMD.exe** 등의 도구를 사용하여 명령줄에 값을 지정하려는 경우 이와 같이 할 수 있습니다.|  
|**CompareUsingTargetCollation={ True &#124; False}**|**False**|이 설정은 배포 중 데이터베이스의 데이터 정렬 처리 방법을 지정합니다.기본적으로 원본에서 지정하는 데이터 정렬과 일치하지 않을 경우 대상 데이터베이스의 데이터 정렬이 업데이트됩니다.  이 옵션을 설정하면 대상 데이터베이스(또는 서버)의 데이터 정렬이 사용됩니다.|  
|**CreateNewDatabase={ True &#124; False}**|**False**|데이터베이스에 게시할 때 대상 데이터베이스를 업데이트할지 또는 삭제 후 다시 만들지 여부를 지정합니다.|  
|**DeployDatabaseInSingleUserMode={ True &#124; False}**|**False**|**True**인 경우 배포 전에 데이터베이스가 단일 사용자 모드로 설정됩니다.|  
|**DisableAndReenableDdlTriggers={True &#124; False}**|**True**|게시 프로세스가 시작할 때 DDL(데이터 정의 언어) 트리거를 사용하지 않고 게시 작업이 끝날 때 다시 사용할지 여부를 지정합니다.|  
|**DoNotAlterChangeDataCaptureObjects={ True &#124; False}**|**True**|**True**인 경우 변경 데이터 캡처 개체가 수정되지 않습니다.|  
|**DoNotAlterReplicatedObjects=( True &#124; False}**|**True**|복제된 개체를 확인 중에 식별할지 여부를 지정합니다.|  
|**DropConstraintsNotInSource= {True &#124; False}**|**True**|데이터베이스에 게시할 때 게시 작업에서 데이터베이스 스냅숏(.dacpac)에 없는 제약 조건을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|  
|**DropDmlTriggersNotInSource= {True &#124; False}**|**True**|데이터베이스에 게시할 때 게시 작업에서 데이터베이스 스냅숏(.dacpac)에 없는 DML(데이터 조작 언어) 트리거를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|  
|**DropExtendedPropertiesNotInSource= {True &#124; False}**|**True**|데이터베이스에 게시할 때 게시 작업에서 데이터베이스 스냅숏(.dacpac)에 없는 확장 속성을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|  
|**DropIndexesNotInSource= {True &#124; False}**|**True**|데이터베이스에 게시할 때 게시 작업에서 데이터베이스 스냅숏(.dacpac)에 없는 인덱스를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|  
|**DropObjectsNotInSource= {True &#124; False}**|**False**|데이터베이스에 게시할 때 데이터베이스 스냅숏(.dacpac) 파일에 없는 개체를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|  
|**DropPermissionsNotInSource= {True &#124; False}**|**False**|데이터베이스에 게시할 때 게시 작업에서 데이터베이스 스냅숏(.dacpac)에 없는 사용 권한을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|  
|**DropRoleMembersNotInSource= {True &#124; False}**|**False**|데이터베이스에 게시할 때 게시 작업에서 데이터베이스 스냅숏(.dacpac)에 없는 역할 멤버를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|  
|**GenerateSmartDefaults={True &#124; False}**|**False**|**SqlPackage.exe**에서 데이터가 들어 있는 테이블을 Null 값을 허용하지 않는 열로 업데이트할 때 자동으로 기본값을 제공할지 여부를 지정합니다.|  
|**IgnoreAnsiNulls= {True &#124; False}**|**False**|데이터베이스에 게시할 때 **ANSI NULLS** 설정의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreAuthorizer= {True &#124; False}**|**False**|데이터베이스에 게시할 때 권한 부여자의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreColumnCollation= {True &#124; False}**|**False**|데이터베이스에 게시할 때 열 데이터 정렬의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreComments= {True &#124; False}**|**False**|데이터베이스에 게시할 때 설명 순서의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreCryptographicProviderFile= {True &#124; False}**|**True**|데이터베이스에 게시할 때 암호화 공급자에 대한 파일 경로의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreDdlTriggerOrder= {True &#124; False}**|**False**|데이터베이스에 게시할 때 DDL(데이터 정의 언어) 트리거 순서의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreDdlTriggerState={True &#124; False}**|**False**|데이터베이스에 게시할 때 DDL 트리거의 사용 또는 사용 안 함 상태의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreDefaultSchema={True &#124; False}**|**False**|데이터베이스에 게시할 때 기본 스키마의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreDmlTriggerOrder= {True &#124; False}**|**False**|데이터베이스에 게시할 때 DML 트리거 순서의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreDmlTriggerState= {True &#124; False}**|**False**|데이터베이스에 게시할 때 DML 트리거의 사용 또는 사용 안 함 상태의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreExtendedProperties= {True &#124; False}**|**False**|데이터베이스에 게시할 때 확장 속성의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreFileAndLogFilePath={True &#124; False}**|**True**|데이터베이스에 게시할 때 파일 및 로그 파일에 대한 경로의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreFilegroupPlacement= {True &#124; False}**|**True**|데이터베이스에 게시할 때 **FILEGROUP** 배치의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreFileSize= {True &#124; False}**|**True**|데이터베이스에 게시할 때 파일 크기의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreFillFactor= {True &#124; False}**|**True**|데이터베이스에 게시할 때 채우기 비율의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
  
|속성|Default|설명|  
|------------|-----------|---------------|  
|**IgnoreFullTextCatalogFilePath= {True &#124; False}**|**True**|데이터베이스에 게시할 때 전체 텍스트 인덱스 파일에 대한 경로의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreIdentitySeed= {True &#124; False}**|**False**|데이터베이스에 게시할 때 ID 열 초기값의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreIncrement= {True &#124; False}**|**False**|데이터베이스에 게시할 때 ID 증가값 열의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreIndexOptions ={True &#124; False}**|**False**|데이터베이스에 게시할 때 인덱스 옵션의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreIndexPadding= {True &#124; False}**|**True**|데이터베이스에 게시할 때 인덱스 패딩의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreKeywordCasing= {True &#124; False}**|**True**|데이터베이스에 게시할 때 키워드 대/소문자 구분의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreLockHintsOnIndexes= {True &#124; False}**|**False**|데이터베이스에 게시할 때 인덱스의 잠금 힌트의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreLoginSids= {True &#124; False}**|**True**|데이터베이스에 게시할 때 SID(보안 식별자)의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreNotForReplication= {True &#124; False}**|**False**|데이터베이스에 게시할 때 복제용 아님 설정의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreObjectPlacementOnPartitionScheme= {True &#124; False}**|**True**|데이터베이스에 게시할 때 파티션 스키마에 대한 개체 배치의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnorePartitionSchemes= {True &#124; False}**|**False**|데이터베이스에 게시할 때 파티션 스키마 및 기능의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnorePermissions= {True &#124; False}**|**False**|데이터베이스에 게시할 때 사용 권한의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreQuotedIdentifiers= {True &#124; False}**|**False**|데이터베이스에 게시할 때 따옴표 붙은 식별자 설정의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreRoleMembership={True &#124; False}**|**False**|데이터베이스에 게시할 때 로그인의 역할 멤버 자격 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreRouteLifetime= {True &#124; False}**|**True**|데이터베이스에 게시할 때 로그인 역할 멤버십의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreSemicolonBetweenState= {True &#124; False}**|**True**|데이터베이스에 게시할 때 Transact-SQL 문 사이의 세미콜론의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreTableOptions= {True &#124; False}**|**False**|데이터베이스에 게시할 때 테이블 옵션의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreUserSettingsObjects= {True &#124; False}**|**False**|데이터베이스에 게시할 때 사용자 설정 옵션의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreWhitespace= {True &#124; False}**|**True**|데이터베이스에 게시할 때 공백의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreWithNocheckOnCheckConstraints={True &#124; False}**|**False**|데이터베이스에 게시할 때 CHECK 제약 조건에 대한 **WITH NOCHECK** 절 값의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IgnoreWithNocheckOnForeignKeys={True &#124; False}**|**False**|데이터베이스에 게시할 때 외래 키에 대한 **WITH NOCHECK** 절 값의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**IncludeCompositeObjects= {True &#124; False}**|**False**|단일 게시 작업의 일부로 모든 복합 요소를 포함할지 여부를 지정합니다.|  
|**IncludeTransactionalScripts={True &#124; False}**|**False**|데이터베이스에 게시할 때 가능하면 언제나 트랜잭션 문을 사용할지 여부를 지정합니다.|  
|**NoAlterStatementsToChangeClrTypes={True &#124; False}**|**False**|차이가 있을 경우 ALTER ASSEMBLY 문을 실행하는 대신 게시에서 항상 어셈블리를 삭제하고 다시 만들지를 지정합니다.|  
|**PopulateFilesOnFilegroups= {True &#124; False}**|**True**|대상 데이터베이스에 새 **FileGroup**을 만들 때 새 파일도 만들지 여부를 지정합니다.|  
|**RegisterDataTierApplication={True &#124; False}**|**False**|스키마가 데이터베이스 서버에 등록되었는지 여부를 지정합니다.|  
|**ScriptDatabaseCollation {True &#124; False}**|**False**|데이터베이스에 게시할 때 데이터베이스 데이터 정렬의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**ScriptDatabaseCompatibility= {True &#124; False}**|**True**|데이터베이스에 게시할 때 데이터베이스 호환성의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|  
|**ScriptDatabaseOptions= {True &#124; False}**|**True**|데이터베이스에 게시할 때 대상 데이터베이스 속성을 설정 또는 업데이트할지 여부를 지정합니다.|  
|**ScriptFileSize={True &#124; False}**|**False**|파일 그룹에 파일을 추가할 때 크기를 지정하는지 여부를 제어합니다.|  
|**ScriptNewConstraintValidation= {True &#124; False}**|**True**|작업 중간에 CHECK 또는 외래 키 제약 조건으로 발생하는 데이터 오류를 방지하도록 모든 제약 조건을 게시 마지막에 하나의 집합으로 확인할지 여부를 지정합니다. 이 옵션이 **False**인 경우 해당 데이터를 확인하지 않고 제약 조건이 게시됩니다.|  
|**ScriptDeployStateChecks={True &#124; False}**|**False**|데이터베이스 및 서버 이름이 데이터베이스 프로젝트에 지정된 이름과 일치하는지 여부를 확인하는 문을 게시 스크립트에 생성할지 여부를 지정합니다.|  
|**ScriptRefreshModule= {True &#124; False}**|**True**|게시 스크립트의 마지막에 refresh 문을 포함할지 여부를 지정합니다.|  
|**Storage={File&#124;Memory}**|**메모리**|데이터베이스 모델을 생성할 때 요소의 저장 방법을 지정합니다. 성능상의 이유로 기본값은 **Memory**입니다. 매우 큰 데이터베이스의 경우 파일 지원 저장소가 필요합니다.|  
|**TreatVerificationErrorsAsWarnings= {True &#124; False}**|**False**|게시 확인 중 발생한 오류를 경고로 처리할지 여부를 지정합니다. 생성된 배포 계획을 대상 데이터베이스에 대해 실행하기 전에 해당 계획에 대한 확인이 수행됩니다. 계획 확인에서 대상 전용 개체(예: 인덱스)가 없는 등의 문제가 발견되면 해당 계획을 삭제하여 변경해야 합니다. 또한 복합 프로젝트에 대한 참조로 인한 종속성(예: 테이블, 뷰)이 존재하지만 대상 데이터베이스에는 존재하지 않는 상황도 확인됩니다. 첫 번째 오류가 발생할 때 게시 작업을 정지하지 않고 확인 오류를 경고로 처리하여 전체 문제 목록을 얻을 수도 있습니다.|  
|**UnmodifiableObjectWarnings= {True &#124; False}**|**True**|개체에서 수정할 수 없는 차이(예: 파일의 파일 경로 또는 파일 크기가 다른 경우)가 발견될 경우 경고를 발생할지 여부를 지정합니다.|  
|**VerifyCollationCompatibility={True &#124; False}**|**True**|데이터 정렬 호환성이 확인되는지 여부를 지정합니다.|  
|**VerifyDeployment={True &#124; False}**|**True**|성공적 게시를 차단할 수 있는 문제가 존재할 경우 게시 작업을 중단하는 검사를 게시 전에 수행할지 여부를 지정합니다. 예를 들어 게시 중 대상 프로젝트에 대상 데이터베이스의 외래 키가 없어 오류가 발생할 경우 게시 작업이 중단될 수 있습니다.|  
  
> [!NOTE]  
> 지정된 대상 매개 변수는 원본 게시 프로필에 지정된 대상 매개 변수를 재정의합니다.  
  
> [!NOTE]  
> **SQLCMD** 변수 및 값은 대상 매개 변수로 지정될 수 없으므로 게시 프로필 원본 매개 변수에 지정해야 합니다.  
  
다음 **대상** 매개 변수는 **DeployReport** 및 **Script** 작업에만 사용할 수 있습니다.  
  
|매개 변수|Default|설명|  
|-------------|-----------|---------------|  
|**OutputPath**={ *string* }|해당 사항 없음|**dbSqlPackage**에 ‘문자열’로 지정된 디스크 위치에 DeployReport XML 출력 파일 또는 Script SQL 출력 파일을 만들도록 지시하는 선택적 매개 변수입니다. 이 작업은 문자열로 지정된 위치에 현재 존재하는 모든 스크립트를 덮어씁니다.|  
  
> [!NOTE]  
> **OutputPath** 매개 변수가 **DeployReport** 또는 **Script** 작업에 제공되지 않은 경우 출력이 메시지로 반환됩니다.  
  
## <a name="examples"></a>예  
다음은 **dbSqlPackage**를 사용하는 **Extract** 작업의 예제 구문입니다.  
  
```  
MSDeploy.exe –verb:sync –source:dbSqlPackage="<source connection string>”,<source parameter> –dest:dbSqlPackage="<target dacpac file path>”  
```  
  
다음은 **dbSqlPackage**를 사용하는 **Publish** 작업의 예제 구문입니다.  
  
```  
MSDeploy.exe –verb:sync –source:dbSqlPackage="<source dacpac file path>" –dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=Publish,<destination parameters>  
```  
  
다음은 **dbSqlPackage**를 사용하는 **DeployReport** 작업의 예제 구문입니다.  
  
```  
MSDeploy.exe –verb:sync –source:dbSqlPackage="<source dacpac file path>" –dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=DeployReport,OutputPath="<path to output XML file>",<destination parameters>  
```  
  
다음은 **dbSqlPackage**를 사용하는 **Script** 작업의 예제 구문입니다.  
  
```  
MSDeploy.exe –verb:sync –source:dbSqlPackage="<source dacpac file path>" –dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=Script,OutputPath="<path to output sql script>",<destination parameters>  
```  
  

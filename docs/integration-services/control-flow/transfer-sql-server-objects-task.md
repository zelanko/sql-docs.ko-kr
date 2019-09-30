---
title: SQL Server 개체 전송 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfersqlserverobjectstask.f1
- sql13.dts.designer.transfersqlserverobjects.general.f1
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f1a2e2122c4d141d8d702d027bf30d65db93f9c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293839"
---
# <a name="transfer-sql-server-objects-task"></a>SQL Server 개체 전송 태스크

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 한 가지 이상 유형의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스 개체를 전송합니다. 예를 들어 이 태스크로 테이블 및 저장 프로시저를 복사할 수 있습니다. 원본으로 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 따라 복사할 수 있는 개체 유형이 달라집니다. 예를 들어 스키마 및 사용자 정의 집계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에만 포함됩니다.  
  
## <a name="objects-to-transfer"></a>전송할 개체  
 전송되는 개체에 대한 사용 권한과 함께 지정된 데이터베이스의 서버 역할, 역할 및 사용자를 복사할 수 있습니다. 개체와 관련된 사용자, 역할 및 사용 권한을 복사하면 전송되는 개체를 대상 서버에서 즉시 작동할 수 있습니다.  
  
 다음 표에서는 복사할 수 있는 개체 유형을 나열합니다.  
  
|Object|  
|------------|  
|테이블|  
|뷰|  
|저장 프로시저|  
|사용자 정의 함수|  
|기본값|  
|사용자 정의 데이터 형식|  
|파티션 함수|  
|파티션 구성표|  
|스키마|  
|어셈블리|  
|사용자 정의 집계|  
|사용자 정의 형식|  
|XML 스키마 컬렉션|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 생성된 UDT(사용자 정의 형식)은 CLR(공용 언어 런타임) 어셈블리에 종속됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 기능을 사용하여 UDT를 전송할 경우 종속 개체를 전송하도록 태스크를 구성해야 합니다. 종속 개체를 전송하려면 **IncludeDependentObjects** 속성을 **True**로 설정합니다.  
  
### <a name="table-options"></a>테이블 옵션  
 테이블을 복사하는 경우 복사 작업에 포함시킬 테이블 관련 항목의 유형을 지정할 수 있습니다. 다음 유형의 항목을 관련 테이블과 함께 복사할 수 있습니다.  
  
-   인덱스  
  
-   트리거  
  
-   전체 텍스트 인덱스  
  
-   기본 키  
  
-   외래 키  
  
 태스크가 생성하는 스크립트가 유니코드 형식인지도 지정할 수 있습니다.  
  
## <a name="destination-options"></a>대상 옵션  
 전송할 때 스키마 이름, 데이터, 전송되는 개체의 확장 속성 및 종속 개체를 포함하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 구성할 수 있습니다. 데이터를 복사할 때는 기존 데이터를 교체 또는 추가할 수 있습니다.  
  
 일부 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에만 적용됩니다. 예를 들어 스키마는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서만 지원됩니다.  
  
## <a name="security-options"></a>보안 옵션  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크에는 원본의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 수준 사용자 및 역할, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 전송되는 개체에 대한 사용 권한을 포함시킬 수 있습니다. 예를 들어 전송되는 테이블에 대한 사용 권한을 전송에 포함시킬 수 있습니다.  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>SQL Server 인스턴스 간 개체 전송  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 및 대상을 지원합니다.  
  
## <a name="events"></a>이벤트  
 태스크는 전송되는 개체에 대해 보고하는 정보 이벤트를 발생시키며 개체를 덮어쓰는 경우 경고 이벤트를 발생시킵니다. 데이터베이스 테이블 잘림과 같은 동작에서도 정보 이벤트가 발생합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크는 개체를 전송하는 진행 과정은 보고하지 않으며 0% 및 100% 완료만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 태스크의 **ExecutionValue** 속성에 저장된 실행 값은 전송된 개체 수를 반환합니다. SQL Server 개체 전송 태스크의 **ExecValueVariable** 속성에 사용자 정의 변수를 할당하면 패키지의 다른 개체에서 개체 전송에 대한 정보를 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 SQL Server 개체 전송 태스크에는 다음 사용자 지정 로그 항목이 포함됩니다.  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   이 로그 항목에서는 전송이 시작되었음을 보고합니다. 로그 항목에 시작 시간이 포함됩니다.  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects    이 로그 항목에서는 전송이 완료되었음을 보고합니다. 로그 항목에 종료 시간이 포함됩니다.  
  
 또한 **OnInformation** 이벤트에 대한 로그 항목에서는 전송하도록 선택한 개체 유형의 개체 수, 전송된 개체의 수 및 테이블로 데이터 전송 시 테이블 잘림과 같은 동작을 보고합니다. 대상에서 덮어쓴 개체마다 **OnWarning** 이벤트에 대한 로그 항목이 기록됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 사용자는 원본 서버에서 개체를 검색하는 권한 및 대상 서버에서 개체를 삭제하고 만드는 권한이 필요하며 무엇보다도 지정된 데이터베이스 및 데이터베이스 개체에 대한 액세스가 필요합니다.  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>SQL Server 개체 전송 태스크 구성  
 모든 개체, 한 유형의 모든 개체 또는 한 유형의 지정된 개체만 전송하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 구성할 수 있습니다. 예를 들어 AdventureWorks 데이터베이스에서 선택한 테이블만 복사하도록 선택할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크가 테이블을 전송하는 경우 테이블과 함께 복사할 테이블 관련 개체 유형을 지정할 수 있습니다. 예를 들어 테이블과 함께 복사할 기본 키를 지정할 수 있습니다.  
  
 전송할 때 스키마 이름, 데이터, 전송된 개체의 확장 속성 및 종속 개체를 포함하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 구성하여 전송되는 개체의 기능을 더욱 향상시킬 수 있습니다. 데이터 복사할 때 기존 데이터를 교체할지 또는 추가할지를 지정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크는 런타임에 두 개의 SMO 연결 관리자를 사용하여 원본 서버 및 대상 서버에 연결합니다. SMO 연결 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크와 별도로 구성된 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크에서 참조됩니다. SMO 연결 관리자는 액세스할 서버 및 사용할 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>SQL Server 개체 전송 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
## <a name="transfer-sql-server-objects-task-editor-general-page"></a>SQL Server 개체 전송 태스크 편집기(일반 페이지)
  **SQL Server 개체 전송 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크의 이름을 지정하고 해당 태스크를 설명할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 만드는 사용자에게는 원본 서버 개체를 복사용으로 선택하기 위한 충분한 권한이 있어야 하며 해당 개체를 전송할 대상 서버 데이터베이스에 대한 액세스 권한도 있어야 합니다.  
  
### <a name="options"></a>옵션  
 **이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크에 사용할 고유 이름을 입력합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크에 대한 설명을 입력합니다.  
  
## <a name="transfer-sql-server-objects-task-editor-objects-page"></a>SQL Server 개체 전송 태스크 편집기(개체 페이지)
  **SQL Server 개체 전송 태스크 편집기** 대화 상자의 **개체** 페이지를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 한 인스턴스에서 다른 인스턴스로 복사하기 위한 속성을 지정할 수 있습니다. 테이블, 뷰, 저장 프로시저 및 사용자 정의 함수와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 복사할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 만드는 사용자에게는 원본 서버 개체를 복사용으로 선택하기 위한 충분한 권한이 있어야 하며 해당 개체를 전송할 대상 서버 데이터베이스에 대한 액세스 권한도 있어야 합니다.  
  
### <a name="static-options"></a>정적 옵션  
 **SourceConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 원본 서버에 대한 새 연결을 만듭니다.  
  
 **SourceDatabase**  
 복사할 개체를 가져올 원본 서버의 데이터베이스를 선택합니다.  
  
 **DestinationConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 대상 서버에 대한 새 연결을 만듭니다.  
  
 **DestinationDatabase**  
 개체를 복사해 넣을 대상 서버의 데이터베이스를 선택합니다.  
  
 **DropObjectsFirst**  
 복사하기 전에 먼저 대상 서버에서 선택한 개체를 삭제할지 여부를 선택합니다.  
  
 **IncludeExtendedProperties**  
 개체를 원본 서버에서 대상 서버로 복사할 때 확장 속성을 포함시킬지 여부를 선택합니다.  
  
 **CopyData**  
 개체를 원본 서버에서 대상 서버로 복사할 때 데이터를 포함시킬지 여부를 선택합니다.  
  
 **ExistingData**  
 데이터를 대상 서버로 복사하는 방법을 지정합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**바꾸기**|대상 서버의 데이터를 덮어씁니다.|  
|**추가**|원본 서버에서 복사한 데이터를 대상 서버의 기존 데이터에 추가합니다.|  
  
> [!NOTE]  
>  **ExistingData** 옵션은 **CopyData** 를 **True**로 설정한 경우에만 사용할 수 있습니다.  
  
 **CopySchema**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 수행하는 동안 스키마를 복사할지 여부를 선택합니다.  
  
> [!NOTE]  
>  **CopySchema** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 사용할 수 있습니다.  
  
 **UseCollation**  
 개체 전송에 원본 서버에서 지정한 데이터 정렬을 포함시킬지 여부를 선택합니다.  
  
 **IncludeDependentObjects**  
 선택한 개체를 복사하면 이 개체에 종속된 다른 개체도 함께 복사되도록 할지 여부를 선택합니다.  
  
 **CopyAllObjects**  
 지정한 원본 데이터베이스의 모든 개체를 복사할지, 아니면 선택한 개체만 복사할지를 선택합니다.  이 옵션을 False로 설정하면 전송할 개체를 선택할 수 있고 **CopyAllObjects**섹션에 동적 옵션이 표시됩니다.  
  
 **ObjectsToCopy**  
 원본 데이터베이스에서 대상 데이터베이스로 복사할 개체를 지정하려면 **ObjectsToCopy** 를 확장합니다.  
  
> [!NOTE]  
>  **ObjectsToCopy** 는 **CopyAllObjects** 를 **False**로 설정한 경우에만 사용할 수 있습니다.  
  
 다음 유형의 개체를 복사하는 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 어셈블리  
  
 파티션 함수  
  
 파티션 구성표  
  
 스키마  
  
 사용자 정의 집계  
  
 사용자 정의 형식  
  
 XML 스키마 컬렉션  
  
 **CopyDatabaseUsers**  
 데이터베이스 사용자를 전송에 포함시킬지 여부를 지정합니다.  
  
 **CopyDatabaseRoles**  
 데이터베이스 역할을 전송에 포함시킬지 여부를 지정합니다.  
  
 **CopySqlServerLogins**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 전송에 포함시킬지 여부를 지정합니다.  
  
 **CopyObjectLevelPermissions**  
 개체 수준 사용 권한을 전송에 포함시킬지 여부를 지정합니다.  
  
 **CopyIndexes**  
 인덱스를 전송에 포함시킬지 여부를 지정합니다.  
  
 **CopyTriggers**  
 트리거를 전송에 포함시킬지 여부를 지정합니다.  
  
 **CopyFullTextIndexes**  
 전체 텍스트 인덱스를 전송에 포함시킬지 여부를 지정합니다.  
  
 **CopyPrimaryKeys**  
 기본 키를 전송에 포함시킬지 여부를 지정합니다.  
  
 **CopyForeignKeys**  
 외래 키를 전송에 포함시킬지 여부를 지정합니다.  
  
 **GenerateScriptsInUnicode**  
 생성된 전송 스크립트가 유니코드 형식인지 여부를 지정합니다.  
  
### <a name="dynamic-options"></a>동적 옵션  
  
#### <a name="copyallobjects--false"></a>CopyAllObjects = False  
 **CopyAllTables**  
 지정한 원본 데이터베이스의 모든 테이블을 복사할지, 아니면 선택한 테이블만 복사할지를 선택합니다.  
  
 **TablesList**  
 **테이블 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllViews**  
 지정한 원본 데이터베이스의 모든 뷰를 복사할지, 아니면 선택한 뷰만 복사할지를 선택합니다.  
  
 **ViewsList**  
 **뷰 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllStoredProcedures**  
 지정한 원본 데이터베이스의 모든 사용자 정의 저장 프로시저를 복사할지, 아니면 선택한 프로시저만 복사할지를 선택합니다.  
  
 **StoredProceduresList**  
 **저장 프로시저 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllUserDefinedFunctions**  
 지정한 원본 데이터베이스의 모든 사용자 정의 함수를 복사할지, 아니면 선택한 UDF만 복사할지를 선택합니다.  
  
 **UserDefinedFunctionsList**  
 **사용자 정의 함수 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllDefaults**  
 지정한 원본 데이터베이스의 모든 기본값을 복사할지, 아니면 선택한 기본값만 복사할지를 선택합니다.  
  
 **DefaultsList**  
 **기본값 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllUserDefinedDataTypes**  
 지정한 원본 데이터베이스의 모든 사용자 정의 데이터 형식을 복사할지, 아니면 선택한 사용자 정의 데이터 형식만 복사할지를 선택합니다.  
  
 **UserDefinedDataTypesList**  
 **사용자 정의 데이터 형식 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllPartitionFunctions**  
 지정한 원본 데이터베이스의 모든 사용자 정의 파티션 함수를 복사할지, 아니면 선택한 파티션 함수만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **PartitionFunctionsList**  
 **파티션 함수 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllPartitionSchemes**  
 지정한 원본 데이터베이스의 모든 파티션 구성표를 복사할지, 아니면 선택한 파티션 구성표만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **PartitionSchemesList**  
 **파티션 구성표 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllSchemas**  
 지정한 원본 데이터베이스의 모든 스키마를 복사할지, 아니면 선택한 스키마만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **SchemasList**  
 **스키마 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllSqlAssemblies**  
 지정한 원본 데이터베이스의 모든 SQL 어셈블리를 복사할지, 아니면 선택한 SQL 어셈블리만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **SqlAssembliesList**  
 **SQL 어셈블리 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllUserDefinedAggregates**  
 지정한 원본 데이터베이스의 모든 사용자 정의 집계를 복사할지, 아니면 선택한 사용자 정의 집계만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **UserDefinedAggregatesList**  
 **사용자 정의 집계 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllUserDefinedTypes**  
 지정한 원본 데이터베이스의 모든 사용자 정의 유형을 복사할지, 아니면 선택한 UDT만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **UserDefinedTypes**  
 **사용자 정의 유형 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllXmlSchemaCollections**  
 지정한 원본 데이터베이스의 모든 XML 스키마 컬렉션을 복사할지, 아니면 선택한 XML 스키마 컬렉션만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **XmlSchemaCollectionsList**  
 **XML 스키마 컬렉션 선택** 대화 상자를 열려면 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [SQL Server 개체 전송 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)   
 [대량 가져오기 또는 대량 내보내기를 위한 데이터 형식&#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  

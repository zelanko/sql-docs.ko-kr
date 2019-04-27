---
title: SQL Server 개체 전송 태스크 편집기 (개체 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects Task Editor
ms.assetid: 8cc09118-70ac-4013-8308-d87f8411ca0c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5a5105e162441375ab011510acb2b7fc6d25bbb4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766216"
---
# <a name="transfer-sql-server-objects-task-editor-objects-page"></a>SQL Server 개체 전송 태스크 편집기(개체 페이지)
  **SQL Server 개체 전송 태스크 편집기** 대화 상자의 **개체** 페이지를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 한 인스턴스에서 다른 인스턴스로 복사하기 위한 속성을 지정할 수 있습니다. 테이블, 뷰, 저장 프로시저 및 사용자 정의 함수와 같은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체를 복사할 수 있습니다. 이 태스크에 대한 자세한 내용은 [Transfer SQL Server Objects Task](control-flow/transfer-sql-server-objects-task.md)를 참조하십시오.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체 전송 태스크를 만드는 사용자에게는 원본 서버 개체를 복사용으로 선택하기 위한 충분한 권한이 있어야 하며 해당 개체를 전송할 대상 서버 데이터베이스에 대한 액세스 권한도 있어야 합니다.  
  
## <a name="static-options"></a>정적 옵션  
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
  
|값|Description|  
|-----------|-----------------|  
|**바꾸기**|대상 서버의 데이터를 덮어씁니다.|  
|**추가**|원본 서버에서 복사한 데이터를 대상 서버의 기존 데이터에 추가합니다.|  
  
> [!NOTE]  
>  **ExistingData** 옵션은 **CopyData** 를 **True**로 설정한 경우에만 사용할 수 있습니다.  
  
 **CopySchema**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체 전송 태스크를 수행하는 동안 스키마를 복사할지 여부를 선택합니다.  
  
> [!NOTE]  
>  **CopySchema** 는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 사용할 수 있습니다.  
  
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
  
 다음 유형의 개체를 복사하는 옵션은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
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
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인을 전송에 포함시킬지 여부를 지정합니다.  
  
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
  
## <a name="dynamic-options"></a>동적 옵션  
  
### <a name="copyallobjects--false"></a>CopyAllObjects = False  
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
 지정한 원본 데이터베이스의 모든 사용자 정의 파티션 함수를 복사할지, 아니면 선택한 파티션 함수만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **PartitionFunctionsList**  
 **파티션 함수 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllPartitionSchemes**  
 지정한 원본 데이터베이스의 모든 파티션 구성표를 복사할지, 아니면 선택한 파티션 구성표만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **PartitionSchemesList**  
 **파티션 구성표 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllSchemas**  
 지정한 원본 데이터베이스의 모든 스키마를 복사할지, 아니면 선택한 스키마만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **SchemasList**  
 **스키마 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllSqlAssemblies**  
 지정한 원본 데이터베이스의 모든 SQL 어셈블리를 복사할지, 아니면 선택한 SQL 어셈블리만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **SqlAssembliesList**  
 **SQL 어셈블리 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllUserDefinedAggregates**  
 지정한 원본 데이터베이스의 모든 사용자 정의 집계를 복사할지, 아니면 선택한 사용자 정의 집계만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **UserDefinedAggregatesList**  
 **사용자 정의 집계 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllUserDefinedTypes**  
 지정한 원본 데이터베이스의 모든 사용자 정의 유형을 복사할지, 아니면 선택한 UDT만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **UserDefinedTypes**  
 **사용자 정의 유형 선택** 대화 상자를 열려면 클릭합니다.  
  
 **CopyAllXmlSchemaCollections**  
 지정한 원본 데이터베이스의 모든 XML 스키마 컬렉션을 복사할지, 아니면 선택한 XML 스키마 컬렉션만 복사할지를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서만 지원됩니다.  
  
 **XmlSchemaCollectionsList**  
 **XML 스키마 컬렉션 선택** 대화 상자를 열려면 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 태스크](control-flow/integration-services-tasks.md)   
 [SQL Server 개체 전송 태스크 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [식 페이지](expressions/expressions-page.md)   
 [대량 가져오기 또는 대량 내보내기를 위한 데이터 형식&#40;SQL Server&#41;](../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  

---
title: "ADO NET 대상 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.adonetdest.f1
- sql13.dts.designer.adonetdest.connection.f1
- sql13.dts.designer.adonetdest.mappings.f1
- sql13.dts.designer.adonetdest.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29e1fd8ede6cc943b1ee41a3b0030b2942169abc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="ado-net-destination"></a>ADO.NET 대상
  ADO.NET 대상은 데이터베이스 테이블이나 뷰를 사용하는 다양한 [!INCLUDE[vstecado](../../includes/vstecado-md.md)]호환 데이터베이스로 데이터를 로드합니다. 이 데이터를 기존 테이블이나 뷰에 로드하는 옵션이 제공되거나 새 테이블을 만들고 데이터를 새 테이블에 로드할 수 있습니다.  
  
 ADO NET 대상을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]에 연결할 수 있습니다. OLE DB를 사용하여 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 연결할 수는 없습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 자세한 내용은 [일반 보안 지침 및 제한 사항(Microsoft Azure SQL Database)](http://go.microsoft.com/fwlink/?LinkId=248228)을 참조하세요.  
  
## <a name="troubleshooting-the-ado-net-destination"></a>ADO.NET 대상 문제 해결  
 ADO.NET 대상이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하여 ADO.NET 대상이 수행하는 외부 데이터 원본에 대한 데이터 저장 문제를 해결할 수 있습니다. ADO.NET 대상이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="configuring-the-ado-net-destination"></a>ADO.NET 대상 구성  
 이 대상은 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자에서는 사용할 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 공급자를 지정합니다. 자세한 내용은 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)를 참조하세요.  
  
 ADO.NET 대상에는 입력 열과 대상 데이터 원본 열 사이의 매핑이 포함되므로 입력 열을 모든 대상 열에 매핑하지 않아도 됩니다. 그러나 일부 대상 열의 속성에서 입력 열을 매핑해야 할 수도 있습니다. 그렇지 않으면 오류가 발생할 수 있습니다. 예를 들어 대상 열에 Null 값이 허용되지 않는 경우에는 입력 열을 해당 대상 열로 매핑해야 합니다. 또한 매핑된 열의 데이터 형식이 호환되어야 합니다. 예를 들어 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 공급자에서 지원하지 않을 경우 문자열 데이터 형식의 입력 열을 숫자 데이터 형식의 대상 열에 매핑할 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터 형식이 이미지로 설정된 열에 텍스트 삽입을 지원하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
>  ADO.NET 대상은 DT_DBTIME 유형으로 설정된 입력 열을 datetime 유형으로 설정된 데이터베이스 열에 매핑하는 작업을 지원하지 않습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 대한 자세한 내용은 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 ADO.NET 대상에는 하나의 일반 입력과 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [ADO.NET 사용자 지정 속성](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="ado-net-destination-editor-connection-manager-page"></a>ADO NET 대상 편집기(연결 관리자 페이지)
  **ADO NET 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 대상에 대한 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결을 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
 **연결 관리자 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 ADO NET 대상이 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ADO NET 대상을 두 번 클릭합니다.  
  
3.  **ADO NET 대상 편집기**에서 **연결 관리자**를 클릭합니다.  
  
### <a name="static-options"></a>정적 옵션  
 **Connection manager**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **ADO.NET 연결 관리자 구성** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **테이블 또는 뷰 사용**  
 목록에서 기존 테이블 또는 뷰를 선택하거나 **새로 만들기**를 클릭하여 새 테이블을 만듭니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블 또는 뷰를 만듭니다.  
  
> [!NOTE]  
>  **새로 만들기**를 클릭하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 저장소를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
 **미리 보기**  
 **쿼리 결과 미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
 **사용 가능한 경우 대량 삽입 사용**  
 <xref:System.Data.SqlClient.SqlBulkCopy> 인터페이스를 사용하여 대량 삽입 작업의 성능을 향상시킬지 여부를 지정합니다.  
  
 <xref:System.Data.SqlClient.SqlConnection> 개체를 반환하는 ADO.NET 공급자만 <xref:System.Data.SqlClient.SqlBulkCopy> 인터페이스의 사용을 지원합니다. .NET Data Provider for SQL Server(SqlClient)는 <xref:System.Data.SqlClient.SqlConnection> 개체를 반환하고, 사용자 지정 공급자는 <xref:System.Data.SqlClient.SqlConnection> 개체를 반환할 수 있습니다.  
  
 .NET Data Provider for SQL Server(SqlClient)를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]에 연결할 수 있습니다.  
  
 **사용 가능한 경우 대량 삽입 사용**을 선택하고 **오류** 옵션을 **행 리디렉션**으로 설정하면 대상에서 오류 출력으로 리디렉션하는 일괄 처리 데이터에 올바른 행이 포함될 수 있습니다. 대량 작업에서 오류 처리에 대한 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요. **오류** 옵션에 대한 자세한 내용은 [ADO NET 대상 편집기&#40;오류 출력 페이지&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)를 참조하세요.  
  
> [!NOTE]  
>  SQL Server 또는 Sybase 원본 테이블에 ID 열이 포함되어 있으면 SQL 실행 태스크를 사용하여 ADO NET 대상 전에 IDENTITY_INSERT를 활성화하고 그 후에 다시 비활성화해야 합니다. (ID 열 속성은 열에 대한 증분 값을 지정합니다. SET IDENTITY_INSERT 문은 원본 테이블의 명시적 값을 대상 테이블의 ID 열에 삽입되도록 합니다.)  
>   
>   SET IDENTITY_INSERT 문 및 데이터 로딩을 성공적으로 실행하려면 다음을 수행해야 합니다.  
>       1. SQL 실행 태스크와 ADO NET 대상에 같은 ADO.NET 연결 관리자를 사용합니다.  
>       2. 연결 관리자에서 **RetainSameConnection** 속성 및 **MultipleActiveResultSets** 속성을 True로 설정합니다.  
>       3. ADO.NET 대상에서 **UseBulkInsertWhenPossible** 속성을 False로 설정합니다.   
>
>  자세한 내용은 [SET IDENTITY_INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) 및 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)를 참조하세요.  
  
## <a name="external-resources"></a>외부 리소스  
 sqlcat.com의 기술 문서 - [Windows Azure SQL Database에 빨리 데이터 로드](http://go.microsoft.com/fwlink/?LinkId=244333)  
  
## <a name="ado-net-destination-editor-mappings-page"></a>ADO NET 대상 편집기(매핑 페이지)
  **ADO NET 대상 편집기** 대화 상자의 **매핑** 페이지를 사용하여 입력 열을 대상 열에 매핑할 수 있습니다.  
  
 **매핑 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 ADO NET 대상이 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ADO NET 대상을 두 번 클릭합니다.  
  
3.  **ADO NET 대상 편집기**에서 **매핑**을 클릭합니다.  
  
### <a name="options"></a>변수  
 **사용 가능한 입력 열**  
 사용 가능한 입력 열 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 입력 열을 대상 열에 매핑합니다.  
  
 **사용 가능한 대상 열**  
 사용 가능한 대상 열의 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 대상 열을 입력 열에 매핑합니다.  
  
 **입력 열**  
 선택한 입력 열을 표시합니다. 출력에서 열을 제외하는 **\<ignore>**를 선택하여 매핑을 제거할 수 있습니다.  
  
 **대상 열**  
 매핑 여부에 관계없이 사용 가능한 각 대상 열을 표시합니다.  
  
## <a name="ado-net-destination-editor-error-output-page"></a>ADO NET 대상 편집기(오류 출력 페이지)
  **ADO NET 대상 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 지정할 수 있습니다.  
  
 **오류 출력 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 ADO NET 대상이 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ADO NET 대상을 두 번 클릭합니다.  
  
3.  **ADO NET 대상 편집기**에서 **오류 출력**을 클릭합니다.  
  
### <a name="options"></a>변수  
 **입력 또는 출력**  
 입력 이름을 표시합니다.  
  
 **열**  
 사용되지 않습니다.  
  
 **오류**  
 오류가 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **관련 항목:** [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **잘림**  
 사용되지 않습니다.  
  
 **설명**  
 작업에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 선택한 모든 셀에 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
  

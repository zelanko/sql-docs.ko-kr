---
title: "ADO NET 대상 편집기 (연결 관리자 페이지) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.adonetdest.connection.f1
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 16ed4103735f389959531b92fad81884fc583a5b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="ado-net-destination-editor-connection-manager-page"></a>ADO NET 대상 편집기(연결 관리자 페이지)
  **ADO NET 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 대상에 대한 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결을 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
 ADO NET 대상에 대한 자세한 내용은 [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md)을 참조하십시오.  
  
 **연결 관리자 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 ADO NET 대상이 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ADO NET 대상을 두 번 클릭합니다.  
  
3.  **ADO NET 대상 편집기**에서 **연결 관리자**를 클릭합니다.  
  
## <a name="static-options"></a>정적 옵션  
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
  
 반환 하는 ADO.NET 공급자만 한 <xref:System.Data.SqlClient.SqlConnection> 개체의 사용을 지원는 <xref:System.Data.SqlClient.SqlBulkCopy> 인터페이스입니다. .NET Data Provider for SQL Server(SqlClient)는 <xref:System.Data.SqlClient.SqlConnection> 개체를 반환하고, 사용자 지정 공급자는 <xref:System.Data.SqlClient.SqlConnection> 개체를 반환할 수 있습니다.  
  
 .NET Data Provider for SQL Server(SqlClient)를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]에 연결할 수 있습니다.  
  
 **사용 가능한 경우 대량 삽입 사용**을 선택하고 **오류** 옵션을 **행 리디렉션**으로 설정하면 대상에서 오류 출력으로 리디렉션하는 일괄 처리 데이터에 올바른 행이 포함될 수 있습니다. 대량 작업에서 오류 처리에 대한 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요. 에 대 한 자세한 내용은 **오류** 옵션 [ADO NET 대상 편집기 &#40; 오류 출력 페이지 &#41; ](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]  
>  SQL Server 또는 Sybase 원본 테이블에서 id 열을 포함 하는 경우 ADO NET 대상 전에 IDENTITY_INSERT를 사용 하도록 설정 하 고 나중에 다시 사용할 수 없도록 SQL 실행 태스크를 사용 해야 합니다. (Identity column 속성 열에 대 한 증분 값을 지정합니다. SET IDENTITY_INSERT 문을 사용 하면 대상 테이블에 id 열에 삽입할 원본 테이블에서 명시적 값.)  
>   
>   SET IDENTITY_INSERT 문 및 데이터를 성공적으로 로드를 실행 하려면 다음을 수행 해야 합니다.
>       1. ADO.NET 대상 및 SQL 실행 태스크에 대 한 동일한 ADO.NET 연결 관리자를 사용 합니다.
>       2. 연결 관리자에서 설정 된 **RetainSameConnection** 속성 및 **MultipleActiveResultSets** 속성을 True로 합니다.
>       3. ADO.NET 대상에서 설정 된 **UseBulkInsertWhenPossible** 속성을 false로 합니다.
>
>  자세한 내용은 [SET IDENTITY_INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) 및 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)를 참조하세요.  
  
## <a name="external-resources"></a>외부 리소스  
 sqlcat.com의 기술 문서 - [Windows Azure SQL Database에 빨리 데이터 로드](http://go.microsoft.com/fwlink/?LinkId=244333)  
  
## <a name="see-also"></a>관련 항목:  
 [ADO NET 대상 편집기&#40;매핑 페이지&#41;](../../integration-services/data-flow/ado-net-destination-editor-mappings-page.md)   
 [ADO NET 대상 편집기 &#40; 오류 출력 페이지 &#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)   
 [ADO.NET 연결 관리자](../../integration-services/connection-manager/ado-net-connection-manager.md)   
 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md)  
  
  

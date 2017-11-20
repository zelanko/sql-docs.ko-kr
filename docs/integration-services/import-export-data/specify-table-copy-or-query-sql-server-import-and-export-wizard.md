---
title: "테이블 복사 또는 쿼리 (SQL Server 가져오기 및 내보내기 마법사)를 지정 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 59820083a0a092fc6704bebd491f1bfc0827732d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>테이블 복사 또는 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사)
  데이터 대상 및 연결하는 방법에 대한 정보를 제공하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **테이블 복사 또는 쿼리 지정**을 표시합니다. 이 페이지에서 다음 옵션 중 하나를 선택합니다.
-   **하나 이상의 테이블 또는 뷰에서 데이터 복사**을 표시합니다. 테이블 또는 목록에서 테이블을 선택 하려고 합니다.
-   **전송 데이터를 지정할 쿼리 작성**을 표시합니다. 입력 하거나 SQL 쿼리 텍스트에 붙여 하려고 합니다.
    
> [!TIP]
> 둘 이상의 데이터베이스나 테이블 및 뷰 이외의 다른 데이터베이스 개체를 복사해야 하는 경우 가져오기 및 내보내기 마법사 대신 데이터베이스 복사 마법사를 사용합니다. 자세한 내용은 [데이터베이스 복사 마법사 사용](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.     
 
## <a name="screen-shot-of-the-specify-table-copy-or-query-page"></a>테이블 복사 또는 쿼리 지정 페이지의 스크린샷    
 다음 스크린샷은 마법사의 **테이블 복사 또는 쿼리 지정** 페이지를 보여 줍니다.    
    
 ![가져오기 및 내보내기 마법사의 테이블 복사 또는 쿼리 페이지](../../integration-services/import-export-data/media/table-copy-or-query.png "가져오기 및 내보내기 마법사의 테이블 복사 또는 쿼리 페이지")    
    
## <a name="specify-whether-to-copy-an-entire-table-or-write-a-query"></a>전체 테이블을 복사할지 또는 쿼리를 작성할지 지정 
 **하나 이상의 테이블 또는 뷰에서 데이터 복사**    
 필터링 또는 레코드를 정렬 하지 않고 소스에서 데이터를 복사 하려면이 옵션을 선택 합니다.   

**하나 이상의 테이블 또는 뷰에서 데이터 복사**를 선택하면 한 테이블 또는 뷰에서 하나의 대상 테이블로 복사하거나 여러 테이블 또는 뷰에서 여러 대상 테이블로 복사할 수 있습니다.

 **다음**을 클릭한 후 **원본 테이블 및 뷰 선택** 페이지에서 복사할 테이블을 선택합니다. 자세한 내용은 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)을 참조하세요.   
    
 **전송 데이터를 지정할 쿼리 작성**    
 대상에 복사하기 전에 원본 데이터를 필터링하거나 정렬하려면 이 옵션을 선택합니다.    
    
**전송 데이터를 지정할 쿼리 작성**을 선택하면 쿼리 결과를 하나의 대상 테이블에만 복사할 수 있습니다.  

**다음**을 클릭한 후 SQL 문을 제공하여 열을 지정하고 **원본 쿼리 지정** 대화 상자에서 행을 선택합니다. 자세한 내용은 [원본 쿼리 지정](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)을 참조하세요.   
    
## <a name="why-isnt-the-copy-option-available"></a>복사 옵션을 사용할 수 없는 이유    
 마법사에서 **데이터 공급자를 사용하여 데이터 원본에 연결하는 경우** 하나 이상의 테이블 또는 뷰에서 데이터 복사 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 옵션을 사용하지 못할 수 있습니다. . 이러한 경우는 마법사에 데이터 원본의 테이블 및 뷰 목록을 요청하는 데 필요한 데이터 공급자 정보가 없을 때 발생합니다. 
 
계속 사용할 수 있습니다는 **는 쿼리를 작성할** 옵션도 경우 내보낼 테이블의 이름을 알고 있는으로 일반적으로 SQL 쿼리를 작성 하지 않습니다. 에 **원본 쿼리 지정** 후 볼 수 있는 대화 상자를 클릭 **다음**,으로 쿼리를 입력 `SELECT * FROM <name of table>`합니다. 테이블의 이름에 공백이 나 기타 특수 문자가 있으면 대괄호-에서 이름을 묶습니다 `SELECT * FROM [<name of table>]`합니다.

### <a name="more-info"></a>추가 정보
 **하나 이상의 테이블 또는 뷰에서 데이터 복사** 옵션은 ProviderDescriptors.xml 파일에 ProviderDescription 섹션이 있는 공급자에 대해서만 사용할 수 있습니다. (기본적으로이 파일은 \< *드라이브*>: files\microsoft SQL Server\130\DTS\ProviderDescriptors.) 이 파일의 각 ProviderDescription 섹션에는 해당 공급자에서 메타데이터를 검색하는 데 필요한 정보가 포함되어 있습니다.    
    
 기본적으로 다음 목록의 공급자에 대해서만 ProviderDescriptors.xml 파일에 ProviderDescription 섹션이 포함됩니다.    
    
-   .Net Framework Data Provider for SQL Server(System.Data.SqlClient)    
    
-   .Net Framework Data Provider for Oracle(System.Data.OracleClient)    
    
-   .Net Framework Data Provider for ODBC(System.Data.Odbc)    
    
-    System.Data.OleDb(모든 OLE DB 공급자에 적용됨)    
    
-   Microsoft Host Integration Server에 의해 설치된 Microsoft Provider for DB2(Microsoft.HostIntegration.MsDb2Client.MsDb2Connection)    
    
 타사 개발자는 ProviderDescriptors.xml 파일에 ProviderDescriptor 섹션을 추가하여 해당 공급자에 **하나 이상의 테이블 또는 뷰에서 데이터 복사** 옵션을 사용할 수 있습니다. ProviderDescriptor 섹션에 대한 요구 사항을 검토하려면 기본적으로 ProviderDescriptors.xml 파일과 같은 폴더에 있는 ProviderDescriptors.xsd 스키마 파일을 참조하세요.    
    
## <a name="whats-next"></a>다음 단계    
 전체 테이블을 복사할지 또는 쿼리를 제공할지 지정한 후 다음 페이지는 이 페이지에서 선택한 옵션과 데이터 대상에 따라 달라집니다.    
    
-   **하나 이상의 테이블 또는 뷰에서 데이터 복사**를 선택한 경우 대부분의 대상에 대한 다음 페이지는 **원본 테이블 및 뷰 선택**입니다. 이 페이지에서는 데이터 원본에서 대상으로 복사할 기존 테이블 및 뷰를 선택합니다. 자세한 내용은 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)을 참조하세요.    
    
-   **하나 이상의 테이블 또는 뷰에서 데이터 복사** 를 선택했으며 대상이 플랫 파일인 경우 다음 페이지는 **플랫 파일 대상 구성**입니다. 이 페이지에서 대상 플랫 파일에 대한 서식 옵션을 지정합니다. 플랫 파일을 구성한 후 다음 페이지는 **원본 테이블 및 뷰 선택**입니다. 자세한 내용은 [플랫 파일 대상 구성](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)을 참조하세요.    
    
-   **전송 데이터를 지정할 쿼리 작성**을 선택한 경우 다음 페이지는 **원본 쿼리 지정**입니다. 이 페이지에서는 데이터 원본에서 대상으로 복사할 데이터를 선택하는 SQL 문을 작성하고 테스트합니다. 쿼리를 지정한 후 다음 페이지는 **원본 테이블 및 뷰 선택**입니다. 자세한 내용은 [원본 쿼리 지정](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)




---
title: 데이터 대량 가져오기 및 내보내기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36065984f03980f54cbc6a75162bb007f8b5f772
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124443"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>데이터 대량 가져오기 및 내보내기(SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는*테이블에서 대량으로 데이터(* 대량 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )를 내보내고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이나 분할되지 않은 뷰로 대량의 데이터를 가져올 수 있습니다. 대량 가져오기 및 대량 내보내기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다른 데이터 원본 간에 데이터를 효과적으로 전송하는 데 필수적입니다. *대량 내보내기* 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 데이터 파일로 복사하는 것입니다. *대량 가져오기* 는 데이터 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터를 로드하는 것입니다. 예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 응용 프로그램의 데이터를 데이터 파일로 내보낸 다음 해당 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 대량으로 가져올 수 있습니다.  
  
 **항목 내용:**  
  
-   [대량 가져오기 및 대량 내보내기 작업 소개](#Intro)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="Intro"></a> 대량 가져오기 및 내보내기 개요  
 이 섹션에서는 데이터 대량 가져오기 및 내보내기에 사용할 수 있는 여러 방법을 나열하고 간단하게 비교합니다. 또한 서식 파일을 소개합니다.  
  
 **항목 내용:**  
  
-   [대량 데이터 가져오기 및 내보내기 방법](#MethodsForBuliIE)  
  
-   [서식 파일](#FFs)  
  
###  <a name="MethodsForBuliIE"></a> 대량 데이터 가져오기 및 내보내기 방법  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 대량의 데이터를 내보내고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이나 분할되지 않은 뷰로 대량의 데이터를 가져올 수 있습니다. 다음과 같은 기본 방법을 사용할 수 있습니다.  
  
|메서드|Description|데이터 가져오기|데이터 내보내기|  
|------------|-----------------|------------------|------------------|  
|[bcp 유틸리티](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|데이터를 대량으로 내보내고 가져오며 서식 파일을 생성하는 명령줄 유틸리티(Bcp.exe)입니다.|사용자 계정 컨트롤|사용자 계정 컨트롤|  
|[BULK INSERT 문](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|데이터 파일에서 데이터베이스 테이블이나 분할되지 않은 뷰로 직접 데이터를 가져오는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.|사용자 계정 컨트롤|아니요|  
|[INSERT ... SELECT * FROM OPENROWSET(BULK...) 문](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|INSERT 문의 데이터를 선택하는 OPENROWSET(BULK…) 함수를 지정하여 대량의 데이터를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 테이블로 가져오기 위해 OPENROWSET 대량 행 집합 공급자를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문입니다.|사용자 계정 컨트롤|아니요|  
  
> [!IMPORTANT]  
>  CSV(쉼표로 구분된 값) 파일은 SQL Server 대량 가져오기 작업에서 지원되지 않습니다. 그러나 경우에 따라 데이터를 SQL Server로 대량으로 가져오기 위한 데이터 파일로 CSV(쉼표로 구분된 값) 파일이 사용될 수 있습니다. CSV 파일의 필드 종결자로는 쉼표 이외에 다른 문자도 사용될 수 있습니다. 자세한 내용은 [대량 내보내기 또는 가져오기를 위한 데이터 준비&#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)를 참조하세요.  
  
###  <a name="FFs"></a> 서식 파일  
 **bcp** 유틸리티, BULK INSERT 및 INSERT ... SELECT \* FROM OPENROWSET(BULK...)은 모두 데이터 파일의 각 필드에 대한 서식 정보를 저장하는 *서식 파일*이라는 특수 파일을 사용하도록 지원합니다. 또한 서식 파일에는 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 대한 정보가 포함되어 있습니다. 서식 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 데이터를 대량으로 내보내거나 SQL Server 인스턴스에서 데이터를 대량으로 가져올 때 필요한 모든 서식 정보를 제공할 수 있습니다.  
  
 서식 파일을 사용하면 가져오기 작업 중 데이터 파일에 있는 데이터의 해석뿐만 아니라 내보내기 작업 중 데이터 파일에 있는 데이터의 서식을 지정할 수 있습니다. 이와 같이 융통성이 있기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 외부 응용 프로그램에 대한 특정 요구 사항에 따라 데이터를 해석하거나 데이터의 서식을 다시 지정하기 위해 특수한 목적의 코드를 작성할 필요가 없습니다. 예를 들어 대량으로 내보낸 데이터를 쉼표로 값을 구분해야 하는 응용 프로그램으로 로드해야 할 경우 서식 파일을 사용하여 내보낸 데이터에서 쉼표를 필드 종결자로 삽입할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 두 종류의 서식 파일, 즉 XML 서식 파일 및 비 XML 서식 파일을 지원합니다.  
  
 서식 파일을 생성할 수 있는 유일한 도구는 **bcp** 유틸리티입니다. 자세한 내용은 [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)를 참조하세요. 서식 파일에 대한 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  대량 내보내기 또는 가져오기 작업 동안 서식 파일이 제공되지 않는 경우 사용자는 명령줄에서 기본 서식 지정을 무시할 수 있습니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [Bcp 유틸리티를 사용 하 여 대량 데이터 내보내기 및 가져오기 &#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)  
  
-   [BULK INSERT 또는 OPENROWSET을 사용 하 여 데이터 대량 가져오기&#40;대량... &#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)  
  
-   [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [대량 내보내기 또는 가져오기를 위한 데이터 준비&#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **서식 파일을 사용하려면**  
  
-   [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면**  
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **bcp를 사용할 때 데이터 형식의 호환 가능성을 지정하려면**  
  
1.  [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [bcp를 사용하여 파일 저장 유형 지정&#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [대량 가져오기의 최소 로깅을 위한 선행 조건](prerequisites-for-minimal-logging-in-bulk-import.md)   
 [데이터를 가져오거나 내보내기 위한 서식 파일 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [데이터베이스를 다른 서버로 복사](../databases/copy-databases-to-other-servers.md)   
 [XML 데이터 대량 로드 수행&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [대량 복사 작업 수행](../native-client/features/performing-bulk-copy-operations.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [데이터를 가져오거나 내보내기 위한 서식 파일 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  

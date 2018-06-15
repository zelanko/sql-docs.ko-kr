---
title: bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 09/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4cef9b1c98ced19606f0e3d2650816a8214f526d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32938178"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기(SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 분할된 뷰를 포함하여 SELECT 문이 작동하는 [데이터베이스의 어디에서나 데이터를 가져올 수 있도록](../../tools/bcp-utility.md) bcp 유틸리티 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하는 방법에 대해 간략하게 설명합니다.  
  
 bcp 유틸리티(Bcp.exe)는 BCP(대량 복사 프로그램) API를 사용하는 명령줄 도구입니다. bcp 유틸리티는 다음 태스크를 수행합니다.  
  
-   데이터 파일로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 대량으로 내보냅니다.  
  
-   쿼리의 데이터를 대량으로 내보냅니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터 파일의 데이터를 대량으로 가져옵니다.  
  
-   서식 파일을 생성합니다.  
  
 **bcp** 명령을 통해 bcp 유틸리티에 액세스합니다. 기존 서식 파일을 사용하지 않는 경우 **bcp** 명령을 사용하여 데이터를 대량으로 가져오려면 테이블의 스키마와 열의 데이터 형식을 이해해야 합니다.  
  
 bcp 유틸리티는 다른 프로그램에서 사용할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 데이터 파일로 내보낼 수 있습니다. 또한 이 유틸리티는 일반적으로 DBMS(데이터베이스 관리 시스템)와 같은 다른 프로그램의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터를 가져올 수 있습니다. 원본 프로그램에서 데이터 파일로 데이터를 내보낸 다음 별도의 작업으로 데이터 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터를 복사합니다.  
  
 **bcp** 명령은 데이터 파일의 데이터 형식과 기타 정보를 지정하는 데 사용하는 스위치를 제공합니다. 이러한 스위치가 지정되지 않은 경우 해당 명령은 데이터 파일의 데이터 필드 유형과 같은 서식 정보를 확인하는 메시지를 표시합니다. 그런 다음 명령은 대화형 응답을 포함하여 서식 파일을 만들 것인지 묻습니다. 나중에 융통성 있게 대량으로 가져오기 또는 내보내기 작업을 수행하려면 서식 파일이 유용합니다. 나중에 해당 데이터 파일에 대해 **bcp** 명령을 실행할 때 서식 파일을 지정할 수 있습니다. 자세한 내용은 [bcp를 사용하여 데이터 형식을 호환 가능하도록 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)을 참조하세요.  
  
>**참고!!** bcp 유틸리티는 ODBC 대량 복사를 사용하여 작성됩니다.
  
 **bcp** 명령 구문에 대한 자세한 내용은 [bcp Utility](../../tools/bcp-utility.md)를 참조하십시오.  
  
## <a name="examples"></a>예  
|다음 항목에는 bcp를 사용하는 예제가 포함되어 있습니다. |
|---|
|[bcp Utility](../../tools/bcp-utility.md)<br /><br />대량 가져오기 또는 대량 내보내기를 위한 데이터 형식(SQL Server)<br />&emsp;&#9679;&emsp;[네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기(SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[문자 형식을 사용하여 데이터 가져오기 또는 내보내기(SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[데이터를 가져오거나 내보내기 위해 유니코드 네이티브 형식 사용(SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[필드 및 행 종결자 지정(SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[대량 가져오기 수행 중 Null 유지 또는 기본값 사용(SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[데이터 대량 가져오기 중 ID 값 유지(SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />데이터를 가져오거나 내보내기 위한 서식 파일(SQL Server)<br />&emsp;&#9679;&emsp;[서식 파일 만들기(SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 데이터 대량 가져오기(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 테이블 열 건너뛰기(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 데이터 필드 건너뛰기(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[XML 문서 대량 가져오기 및 내보내기 예(SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>                                                                                                                                                                                                                  </p>|

  
## <a name="more-examples-and-information"></a>추가 예제 및 정보  
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [대량 데이터 가져오기 준비&#40;SQL Server&#41;](../../relational-databases/import-export/prepare-to-bulk-import-data-sql-server.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
  

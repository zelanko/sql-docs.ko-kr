---
title: bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dd68505153eb43d826f3854bd4f525ed06ea072a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103353"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기(SQL Server)
  이 항목에서는 분할된 뷰를 포함하여 SELECT 문이 작동하는 [데이터베이스의 어디에서나 데이터를 가져올 수 있도록](../../tools/bcp-utility.md) bcp 유틸리티 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하는 방법에 대해 간략하게 설명합니다.  
  
 bcp 유틸리티(Bcp.exe)는 BCP(대량 복사 프로그램) API를 사용하는 명령줄 도구입니다. bcp 유틸리티는 다음 태스크를 수행합니다.  
  
-   데이터 파일로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 대량으로 내보냅니다.  
  
-   쿼리의 데이터를 대량으로 내보냅니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터 파일의 데이터를 대량으로 가져옵니다.  
  
-   서식 파일을 생성합니다.  
  
 **bcp** 명령을 통해 bcp 유틸리티에 액세스합니다. 기존 서식 파일을 사용하지 않는 경우 **bcp** 명령을 사용하여 데이터를 대량으로 가져오려면 테이블의 스키마와 열의 데이터 형식을 이해해야 합니다.  
  
 bcp 유틸리티는 다른 프로그램에서 사용할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 데이터 파일로 내보낼 수 있습니다. 또한 이 유틸리티는 일반적으로 DBMS(데이터베이스 관리 시스템)와 같은 다른 프로그램의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터를 가져올 수 있습니다. 원본 프로그램에서 데이터 파일로 데이터를 내보낸 다음 별도의 작업으로 데이터 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터를 복사합니다.  
  
 **bcp** 명령은 데이터 파일의 데이터 형식과 기타 정보를 지정하는 데 사용하는 스위치를 제공합니다. 이러한 스위치가 지정되지 않은 경우 해당 명령은 데이터 파일의 데이터 필드 유형과 같은 서식 정보를 확인하는 메시지를 표시합니다. 그런 다음 명령은 대화형 응답을 포함하여 서식 파일을 만들 것인지 묻습니다. 나중에 융통성 있게 대량으로 가져오기 또는 내보내기 작업을 수행하려면 서식 파일이 유용합니다. 나중에 해당 데이터 파일에 대해 **bcp** 명령을 실행할 때 서식 파일을 지정할 수 있습니다. 자세한 내용은 [bcp를 사용하여 데이터 형식을 호환 가능하도록 지정&#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  bcp 유틸리티가 ODBC 대량 복사를 사용하여 작성됨  
  
 **bcp** 명령 구문에 대한 자세한 내용은 [bcp Utility](../../tools/bcp-utility.md)를 참조하십시오.  
  
## <a name="examples"></a>예  
 **bcp** 예제는 다음을 참조하세요.  
  
-   [bcp 유틸리티](../../tools/bcp-utility.md)  
  
-   [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [SELECT 절&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-clause-transact-sql)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [대량 데이터 가져오기 준비&#40;SQL Server&#41;](prepare-to-bulk-import-data-sql-server.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
  

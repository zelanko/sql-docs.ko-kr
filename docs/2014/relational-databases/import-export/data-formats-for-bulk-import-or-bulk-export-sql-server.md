---
title: 대량 가져오기 또는 대량 내보내기를 위한 데이터 형식(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 676b5a8d8d05c5cb26a30eaa1b1fe9426ac30ea7
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510038"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>대량 가져오기 또는 대량 내보내기를 위한 데이터 형식(SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 문자 데이터 형식 또는 네이티브 이진 데이터 형식으로 데이터를 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 다른 애플리케이션(예: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) 또는 다른 데이터베이스 서버(예: Oracle 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 간에 데이터를 이동할 때 문자 형식을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 간에 데이터를 전송할 때만 네이티브 형식을 사용할 수 있습니다.  
  
 **항목 내용**  
  
-   [대량 내보내기 또는 가져오기를 위한 데이터 형식](#ComponentsAndConcepts)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> 대량 내보내기 또는 가져오기를 위한 데이터 형식  
 다음 표에서는 데이터 표시 방식 및 작업의 원본 또는 대상에 따라 일반적으로 적절히 사용할 수 있는 데이터 형식을 보여 줍니다.  
  
|연산|네이티브|유니코드 네이티브|문자|유니코드 문자|  
|---------------|------------|--------------------|---------------|-----------------------|  
|확장 또는 DBCS(더블바이트 문자 집합) 문자가 들어 있지 않는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다수 인스턴스 간에 데이터를 대량으로 전송합니다. 서식 파일을 사용하지 않는 한 테이블을 동일하게 정의해야 합니다.|예<sup>1</sup>|-|-|-|  
|`sql_variant` 열의 경우 문자 또는 유니코드 형식과는 달리 네이티브 데이터 형식이 각 `sql_variant` 값에 대해 메타데이터를 보존하기 때문에 네이티브 데이터 형식을 사용하는 것이 가장 좋습니다.|사용자 계정 컨트롤|-|-|-|  
|확장 또는 DBCS 문자가 들어 있는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다수 인스턴스 간에 데이터를 대량으로 전송합니다.|-|사용자 계정 컨트롤|-|-|  
|다른 프로그램으로 생성된 텍스트 파일에서 데이터를 대량으로 가져옵니다.|-|-|사용자 계정 컨트롤|-|  
|다른 프로그램에서 사용할 텍스트 파일로 데이터를 대량으로 내보냅니다.|-|-|사용자 계정 컨트롤|-|  
|유니코드 데이터가 들어 있으나 확장 또는 DBCS 문자는 들어 있지 않는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다수 인스턴스 간에 데이터를 대량으로 전달합니다.|-|-|-|사용자 계정 컨트롤|  
  
 <sup>1</sup> 데이터를 대량으로 내보내는 가장 빠른 방법 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하는 경우 **bcp**합니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [원시 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [데이터를 가져오거나 내보내기 위해 유니코드 원시 형식 사용&#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [bcp를 사용하여 데이터 형식을 호환 가능하도록 지정&#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  

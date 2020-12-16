---
title: 대량 가져오기 및 대량 내보내기를 위한 데이터 형식
description: SQL Server에서는 문자 형식 또는 원시 이진 형식의 데이터를 사용할 수 있습니다. SQL Server와 다른 앱 간에는 문자 형식을 사용하고, SQL Server 인스턴스 간에는 원시 형식을 사용합니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 3a043b45749674d09cd47bfc62eea7d7f70647ee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474054"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>대량 가져오기 또는 대량 내보내기를 위한 데이터 형식(SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 문자 데이터 형식 또는 네이티브 이진 데이터 형식으로 데이터를 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 다른 애플리케이션(예: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) 또는 다른 데이터베이스 서버(예: Oracle 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 간에 데이터를 이동할 때 문자 형식을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 간에 데이터를 전송할 때만 네이티브 형식을 사용할 수 있습니다.  
  
 **항목 내용:**  
  
-   [대량 내보내기 또는 가져오기를 위한 데이터 형식](#ComponentsAndConcepts)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="data-formats-for-bulk-import-or-export"></a><a name="ComponentsAndConcepts"></a> 대량 내보내기 또는 가져오기를 위한 데이터 형식  
 다음 표에서는 데이터 표시 방식 및 작업의 원본 또는 대상에 따라 일반적으로 적절히 사용할 수 있는 데이터 형식을 보여 줍니다.  
  
|작업(Operation)|네이티브|유니코드 네이티브|문자|유니코드 문자|  
|---------------|------------|--------------------|---------------|-----------------------|  
|확장 또는 DBCS(더블바이트 문자 집합) 문자가 들어 있지 않는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다수 인스턴스 간에 데이터를 대량으로 전송합니다. 서식 파일을 사용하지 않는 한 테이블을 동일하게 정의해야 합니다.|예*|-|-|-|  
|**sql_variant** 열의 경우 문자 또는 유니코드 형식과는 달리 원시 데이터 형식이 각 **sql_variant** 값에 대해 메타데이터를 보존하기 때문에 원시 데이터 형식을 사용하는 것이 가장 좋습니다.|예|-|-|-|  
|확장 또는 DBCS 문자가 들어 있는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다수 인스턴스 간에 데이터를 대량으로 전송합니다.|-|예|-|-|  
|다른 프로그램으로 생성된 텍스트 파일에서 데이터를 대량으로 가져옵니다.|-|-|예|-|  
|다른 프로그램에서 사용할 텍스트 파일로 데이터를 대량으로 내보냅니다.|-|-|예|-|  
|유니코드 데이터가 들어 있으나 확장 또는 DBCS 문자는 들어 있지 않는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다수 인스턴스 간에 데이터를 대량으로 전달합니다.|-|-|-|예|  
  
 \*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bcp **를 사용하는 경우** 에서 데이터를 대량으로 내보내는 가장 빠른 방법입니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [bcp를 사용하여 데이터 형식을 호환 가능하도록 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  

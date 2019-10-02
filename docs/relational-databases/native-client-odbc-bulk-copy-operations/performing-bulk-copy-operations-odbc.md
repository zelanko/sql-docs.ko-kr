---
title: 대량 복사 작업 수행 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC]
- ODBC, bulk copy operations
- minimally logged operations [SQL Server Native Client]
- bulk copy [ODBC], about bulk copy
ms.assetid: 5c793405-487c-4f52-88b8-0091d529afb3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ad2e6e418213afcbf00223798c857967581cef0c
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708063"
---
# <a name="performing-bulk-copy-operations-odbc"></a>대량 복사 작업 수행(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 표준에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 복사 작업을 직접 지원하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 이상 버전의 인스턴스에 연결되어 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 복사 작업을 수행하는 DB-Library 함수를 지원합니다. 이 드라이버 관련 확장은 대량 복사 함수를 사용하는 기존 DB-Library 애플리케이션에 대해 편리한 업그레이드 경로를 제공합니다. 특별한 대량 복사 지원은 다음 파일에 포함되어 있습니다.  
  
-   sqlncli.h  
  
     대량 복사 함수를 위한 함수 프로토타입 및 상수 정의를 포함합니다. sqlncli.h는 대량 복사 작업을 수행하는 ODBC 애플리케이션에 포함되어야 하며 애플리케이션을 컴파일할 때 애플리케이션의 포함 경로에 있어야 합니다.  
  
-   sqlncli11.lib  
  
     링커의 라이브러리 경로에 있어야 하며 링크할 파일로 지정해야 합니다. sqlncli11.lib는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 함께 배포됩니다.  
  
-   sqlncli11.dll  
  
     실행 단계에 있어야 합니다. sqlncli11.dll은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 함께 배포됩니다.  
  
> [!NOTE]  
>  ODBC **SQLBulkOperations** 함수는 @no__t 1 대량 복사 함수와 관계가 없습니다. 애플리케이션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 대량 복사 함수를 사용하여 대량 복사 작업을 수행해야 합니다.  
  
## <a name="minimally-logging-bulk-copies"></a>최소로 기록된 대량 복사  
 전체 복구 모델을 사용하면 대량 로드로 수행되는 모든 행 삽입 작업이 트랜잭션 로그에 기록됩니다. 많은 양의 데이터를 로드하는 경우 트랜잭션 로그가 빠르게 채워질 수 있습니다. 특정 조건에서 최소 로깅을 사용할 수 있습니다. 최소 로깅은 대량 로드 작업으로 인해 로그 공간이 채워질 가능성을 줄이며 전체 로깅보다 효율적입니다.  
  
 최소 로깅을 사용 하는 방법에 대 한 자세한 내용은 [대량 가져오기의 최소 로깅을 위한 필수 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조 하세요.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 bcp.exe를 사용하는 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전에는 오류가 발생하지 않았던 상황에서 오류가 표시될 수도 있습니다. 이는 이후 버전에서 bcp.exe가 더 이상 암시적 데이터 형식 변환을 수행하지 않기 때문입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전에는 대상 테이블에 money 데이터 형식이 있을 경우 bcp.exe에서 숫자 데이터를 money 데이터 형식으로 변환했습니다. 하지만 이 경우 bcp.exe에서 단순히 추가 필드를 자르기만 했습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 파일과 대상 테이블의 데이터 형식이 일치하지 않을 경우 대상 테이블에 맞게 잘라야 하는 데이터가 있으면 bcp.exe에서 오류를 발생시킵니다. 이 오류를 해결하려면 대상 데이터 형식과 일치하도록 데이터를 수정합니다. 필요에 따라 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전 릴리스의 bcp.exe를 사용합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 파일 및 서식 파일 사용](../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
-   [프로그램 변수에서 대량 복사](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-from-program-variables.md)  
  
-   [대량 복사 일괄 처리 크기 관리](../../relational-databases/native-client-odbc-bulk-copy-operations/managing-bulk-copy-batch-sizes.md)  
  
-   [텍스트 및 이미지 데이터 대량 복사](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-text-and-image-data.md)  
  
-   [DB-Library에서 ODBC 대량 복사로 변환](../../relational-databases/native-client-odbc-bulk-copy-operations/converting-from-db-library-to-odbc-bulk-copy.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  

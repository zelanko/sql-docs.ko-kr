---
title: 데이터 대량 가져오기 및 내보내기(SQL Server) | Microsoft 문서
description: SQL Server는 SQL Server 테이블에서 데이터를 대량으로 내보내고, SQL Server 테이블이나 분할되지 않은 뷰로 대량 데이터를 가져오는 기능을 지원합니다.
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8429b376cee1b701d95320ecc202daa66155419d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480134"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>데이터 대량 가져오기 및 내보내기(SQL Server)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 *테이블에서 대량으로 데이터(* 대량 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )를 내보내고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이나 분할되지 않은 뷰로 대량의 데이터를 가져올 수 있습니다.

- *대량 내보내기* 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 데이터를 데이터 파일로 복사하는 것입니다.
- *대량 가져오기* 는 데이터 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터를 로드하는 것입니다. 예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 애플리케이션의 데이터를 데이터 파일로 내보낸 다음 해당 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 대량으로 가져올 수 있습니다.

## <a name="methods-for-bulk-importing-and-exporting-data"></a><a name="MethodsForBuliIE"></a> 데이터 대량 가져오기 및 내보내기 방법

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 대량의 데이터를 내보내고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이나 분할되지 않은 뷰로 대량의 데이터를 가져올 수 있습니다. 다음과 같은 기본 방법을 사용할 수 있습니다.

|방법|Description|데이터 가져오기|데이터 내보내기|
|------------|-----------------|------------------|------------------|
|[bcp 유틸리티](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|데이터를 대량으로 내보내고 가져오며 서식 파일을 생성하는 명령줄 유틸리티(Bcp.exe)입니다.|예|예|
|[BULK INSERT 문](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|데이터 파일에서 데이터베이스 테이블이나 분할되지 않은 뷰로 직접 데이터를 가져오는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.|예|예|
|[INSERT ... SELECT * FROM OPENROWSET(BULK...) 문](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|INSERT 문의 데이터를 선택하는 OPENROWSET(BULK…) 함수를 지정하여 대량의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 가져오기 위해 OPENROWSET 대량 행 집합 공급 기업을 사용하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.|예|예|
|[SQL Server 가져오기 및 내보내기 마법사](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)|이 마법사는 데이터베이스, 스프레드시트, 텍스트 파일 등 많은 일반적인 데이터 형식 간에 데이터를 가져오고 내보내는 간단한 패키지를 만듭니다.|예|예|

> [!IMPORTANT]
> SQL Server에 데이터를 대량으로 가져오기 위한 데이터 파일로 CSV (쉼표로 구분된 값) 파일을 사용하는 방법에 대한 규칙은 [대량 내보내기 또는 가져오기를 위한 데이터 준비(SQL Server) ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)를 참조하세요.

> [!NOTE]
> 구분된 파일을 내보내고 가져오는 경우 Azure Synapse Analytics에서는 bcp 유틸리티만 지원됩니다.

## <a name="format-files"></a><a name="FFs"></a> 서식 파일

[bcp 유틸리티](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 및 [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)은 모두 데이터 파일의 각 필드에 대한 서식 정보를 저장하는 *서식 파일* 이라는 특수 파일 사용을 지원합니다. 또한 서식 파일에는 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 대한 정보가 포함되어 있습니다. 서식 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 데이터를 대량으로 내보내거나 SQL Server 인스턴스에서 데이터를 대량으로 가져올 때 필요한 모든 서식 정보를 제공할 수 있습니다.

> [!IMPORTANT]
> BCP를 사용하여 Azure Blob Storage로 데이터를 내보내거나 Azure Blob Storage의 데이터를 Azure SQL Database로 가져올 수는 없습니다. [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 또는 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)를 사용하여 Azure Blob Storage로 내보내거나 가져옵니다.

서식 파일을 사용하면 가져오기 작업 중 데이터 파일에 있는 데이터의 해석뿐만 아니라 내보내기 작업 중 데이터 파일에 있는 데이터의 서식을 지정할 수 있습니다. 이와 같이 융통성이 있기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 외부 애플리케이션에 대한 특정 요구 사항에 따라 데이터를 해석하거나 데이터의 서식을 다시 지정하기 위해 특수한 목적의 코드를 작성할 필요가 없습니다. 예를 들어 대량으로 내보낸 데이터를 쉼표로 값을 구분해야 하는 애플리케이션으로 로드해야 할 경우 서식 파일을 사용하여 내보낸 데이터에서 쉼표를 필드 종결자로 삽입할 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다음과 같은 두 종류의 서식 파일을 지원합니다. XML 서식 파일 및 비 XML 서식 파일.

서식 파일을 생성할 수 있는 유일한 도구는 [bcp 유틸리티](../../tools/bcp-utility.md) 입니다. 자세한 내용은 [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요. 서식 파일에 대한 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.

> [!NOTE]
> 대량 내보내기 또는 가져오기 작업 동안 서식 파일이 제공되지 않는 경우 사용자는 명령줄에서 기본 서식 지정을 무시할 수 있습니다.

|관련 항목|
|---|
|[대량 내보내기 또는 가져오기를 위한 데이터 준비(SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)|
|[대량 가져오기 또는 대량 내보내기를 위한 데이터 형식(SQL Server)](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)<br />&emsp;&#9679;&emsp;[네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기(SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[문자 형식을 사용하여 데이터 가져오기 또는 내보내기(SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[데이터를 가져오거나 내보내기 위해 유니코드 네이티브 형식 사용(SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)|
|[bcp를 사용하여 데이터 형식을 호환 가능하도록 지정(SQL Server)](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[bcp를 사용하여 File Storage 유형 지정(SQL Server)](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[bcp를 사용하여 데이터 파일에 접두사 길이 지정(SQL Server)](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[bcp를 사용하여 필드 길이 지정(SQL Server)](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[필드 및 행 종결자 지정(SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)|
|[대량 가져오기 수행 중 Null 유지 또는 기본값 사용(SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)|
|[데이터 대량 가져오기 중 ID 값 유지(SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)|
|[데이터를 가져오거나 내보내기 위한 서식 파일(SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일 만들기(SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 데이터 대량 가져오기(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 테이블 열 건너뛰기(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 데이터 필드 건너뛰기(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑(SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)|

## <a name="more-information"></a>자세한 정보

- [대량 가져오기의 최소 로깅을 위한 필수 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)
- [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
- [데이터베이스를 다른 서버로 복사](../../relational-databases/databases/copy-databases-to-other-servers.md)
- [XML 데이터 대량 로드 수행&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)
- [대량 복사 작업 수행](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)

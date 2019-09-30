---
title: 대상 선택(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 86b2cf26c7af957579c5368ed70262e43db005f1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285873"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>대상 선택(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 데이터 원본 및 연결하는 방법에 대한 정보를 제공하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **대상 선택**을 표시합니다. 이 페이지에서는 데이터 대상 및 연결하는 방법에 대한 정보를 제공합니다.
  
사용할 수 있는 데이터 대상에 대한 자세한 내용은 [어떤 데이터 원본 및 대상을 사용할 수 있나요?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)를 참조하세요. 

## <a name="screen-shot-of-the-destination-page"></a>대상 페이지의 스크린샷
다음 스크린샷은 마법사의 **대상 선택** 페이지의 첫 번째 부분을 보여 줍니다. 페이지의 나머지 부분에는 여기에서 선택한 대상에 따라 다양한 옵션이 있습니다.

![대상 선택](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>대상 선택
 **대상**  
 데이터를 대상으로 가져올 수 있는 데이터 공급자를 선택하여 대상을 지정합니다.
 
-   일반적으로 공급자 이름에 대상 이름이 포함되어 있기 때문에 **필요한 데이터 공급자는 이름만으로 분명**합니다. 예: *플랫 파일* 대상, Microsoft *Excel*, Microsoft *Access*, .Net Framework Data Provider for *SqlServer*, .Net Framework Data Provider for *Oracle*.

-   **대상에 대한 ODBC 드라이버가 있는 경우** .Net Framework Data Provider for ODBC를 선택합니다. 그런 다음 드라이버 관련 정보를 입력합니다. ODBC 드라이버는 대상의 드롭다운 목록에 표시되지 않습니다. .Net Framework Data Provider for ODBC는 ODBC 드라이버 주위에서 래퍼로 작동합니다. 자세한 내용은 [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.

-   **대상에 사용할 수 있는 공급자가 여러 개 있을 수 있습니다.** 일반적으로 대상에서 작동하는 모든 공급자를 선택할 수 있습니다. 예를 들어 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하려면 .NET Framework Data Provider for SQL Server 또는 SQL Server ODBC를 사용할 수 있습니다. (다른 공급자도 여전히 목록에 있지만 더 이상 지원되지 않습니다.) 

## <a name="my-destination-isnt-in-the-list"></a>내 대상이 목록에 없음
-   Microsoft 또는 타사의 **데이터 공급자를 다운로드해야 할 수도 있습니다**. **대상** 목록에서 사용 가능한 데이터 공급자 목록은 컴퓨터에 설치된 공급자만 포함됩니다. 사용할 수 있는 대상에 대한 자세한 내용은 [어떤 데이터 원본 및 대상을 사용할 수 있나요?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)를 참조하세요.

-   **대상에 대한 ODBC 드라이버가 있나요?** ODBC 드라이버는 대상의 드롭다운 목록에 표시되지 않습니다. 대상에 대한 ODBC 드라이버가 있는 경우 .Net Framework Data Provider for ODBC를 선택합니다. 그런 다음 드라이버 관련 정보를 입력합니다. .Net Framework Data Provider for ODBC는 ODBC 드라이버 주위에서 래퍼로 작동합니다. 자세한 내용은 [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)을 참조하세요.

-   **64비트 및 32비트 공급자.** 64비트 마법사를 실행 중인 경우 32비트 공급자만 설치된 대상은 표시되지 않으며 반대의 경우도 마찬가지입니다.

> [!NOTE]
> 64비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용하려면 SQL Server를 설치해야 합니다. SSDT(SQL Server Data Tools) 및 SSMS(SQL Server Management Studio)는 32비트 애플리케이션이며, 32비트 버전의 마법사를 포함하여 32비트 파일만 설치합니다.

## <a name="after-you-choose-a-destination"></a>대상을 선택한 후
대상을 선택한 후 **대상 선택** 페이지의 나머지에 대해 표시되는 옵션 수는 선택한 데이터 공급자에 따라 달라집니다.

일반적으로 사용되는 대상에 연결하려면 다음 페이지 중 하나를 참조하세요.
-   [SQL Server에 연결](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle에 연결](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [플랫 파일(텍스트 파일)에 연결](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel에 연결](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Access에 연결](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [ODBC를 사용하여 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob Storage에 연결](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [PostgreSQL에 연결](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL에 연결](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

여기에 나열되지 않은 대상에 연결하는 방법에 대한 자세한 내용은 [연결 문자열 참조](https://www.connectionstrings.com/)를 참조하세요. 이 타사 사이트에는 샘플 연결 문자열과 필요한 데이터 공급자 및 연결 정보에 대한 추가 정보가 포함되어 있습니다.

## <a name="whats-next"></a>다음 단계  
 데이터 대상 및 연결하는 방법에 대한 정보를 제공한 후 다음 페이지는 **테이블 복사 또는 쿼리 지정**입니다. 이 페이지에서는 전체 테이블을 복사할지 또는 특정 행만 복사할지 지정합니다. 자세한 내용은 [테이블 복사 또는 쿼리 지정](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)을 참조하세요.  

## <a name="see-also"></a>관련 항목:
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



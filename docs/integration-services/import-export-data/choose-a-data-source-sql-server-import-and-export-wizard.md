---
title: "데이터 원본 (SQL Server 가져오기 및 내보내기 마법사)를 선택 합니다. | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 80d35cb294fd900611c73ca37bba2a66baef0767
ms.contentlocale: ko-kr
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>데이터 원본 선택(SQL Server 가져오기 및 내보내기 마법사)
  시작 페이지 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사가 **데이터 원본 선택**을 표시합니다. 이 페이지에서는 데이터 원본 및 데이터 원본에 연결하는 방법에 대한 정보를 제공합니다.
  
사용할 수 있는 데이터 원본에 대한 자세한 내용은 [어떤 데이터 원본 및 대상을 사용할 수 있나요?](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)를 참조하세요.

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>데이터 원본 선택 페이지의 스크린샷 
다음 스크린샷은 마법사의 **데이터 원본 선택** 페이지의 첫 번째 부분을 보여 줍니다. 페이지의 나머지에 따라 달라 여기에서 선택한 데이터 원본에 따라 달라 지는 옵션입니다.

![원본 선택](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>데이터 원본 선택
 **데이터 원본**  
원본에 연결할 수 있는 데이터 공급자를 선택하여 데이터 원본을 지정합니다.

-   **필요한 데이터 공급자는 일반적으로 이름 만으로는 명확**공급자의 이름을 일반적으로 포함 되어 있으므로 데이터 소스-의 이름 예를 들어, *플랫 파일* 소스, Microsoft *Excel*, Microsoft *액세스*,.Net Framework Data Provider for *SqlServer*,.Net Framework Data Provider for *Oracle*합니다.

-   **데이터 원본에 대 한 ODBC 드라이버가 있는 경우**, 선택 된.Net Framework Data Provider for ODBC 합니다. 드라이버 관련 정보를 입력 합니다. ODBC 드라이버는 데이터 원본의 드롭 다운 목록에 나열 되지 않습니다. .NET Framework Data Provider for ODBC는 ODBC 드라이버 주위에서 래퍼로 작동합니다. 자세한 내용은 참조 하십시오. [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)합니다.

-   **데이터 원본에 사용할 수 있는 공급자가 여러 개 있을 수 있습니다.** 일반적으로 원본에서 작동하는 모든 공급자를 선택할 수 있습니다. 예를 들어, Microsoft에 연결 하는 데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL Server 또는 SQL Server ODBC 드라이버에 대 한.NET Framework Data Provider를 사용할 수 있습니다. (다른 공급자 목록에도 여전히 포함 되어 있지만 이상 지원 되지 않습니다.) 

## <a name="my-data-source-isnt-in-the-list"></a>목록에 없으면 데이터 원본
-   **데이터 공급자를 다운로드 해야 할 수** Microsoft 또는 타사에서 합니다. 사용 가능한 데이터 공급자 목록에서 **데이터 원본** 목록에는 컴퓨터에 설치 된 공급자만 포함 됩니다. 사용할 수 있는 데이터 원본에 대한 자세한 내용은 [어떤 데이터 원본 및 대상을 사용할 수 있나요?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)를 참조하세요.

-   **데이터 원본에 대 한 ODBC 드라이버가 있습니까?** ODBC 드라이버는 데이터 원본의 드롭 다운 목록에 나열 되지 않습니다. 데이터 원본에 대 한 ODBC 드라이버를 설정한 경우 선택 된.Net Framework Data Provider for ODBC 합니다. 드라이버 관련 정보를 입력 합니다. .NET Framework Data Provider for ODBC는 ODBC 드라이버 주위에서 래퍼로 작동합니다. 자세한 내용은 참조 하십시오. [ODBC 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)합니다.

-   **64 비트 및 32 비트 공급자입니다.** 64 비트 마법사를 실행 하는 경우 데이터 소스 표시 되지 않습니다는 32 비트 공급자가 설치 된, 그 반대의 합니다.

> [!NOTE]
> 64 비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용 하려면 SQL Server를 설치 해야 합니다. SQL Server Data Tools (SSDT) 및 SQL Server Management Studio (SSMS)는 32 비트 응용 프로그램 및 32 비트 버전의 마법사를 포함 하 여 32 비트 파일을 설치 합니다.

## <a name="after-you-choose-a-data-source"></a>데이터 원본을 선택한 후
나머지 데이터 소스를 선택한 후는 **데이터 원본을 선택** 페이지는 사용자가 선택한 데이터 공급자에 따라 달라 지는 옵션의 다양 한 수입니다.

를 자주 사용 되는 데이터 원본에 연결 하려면 다음 페이지 중 하나를 참조 합니다.
-   [SQL Server에 연결](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle에 연결](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [플랫 파일 (텍스트 파일)에 연결](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel에 연결](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Access에 연결](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [ODBC를 사용 하 여 연결](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob 저장소에 연결](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [PostgreSQL에 연결](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL에 연결](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

여기에 나열 되어 있지 않은 데이터 원본에 연결 하는 방법에 대 한 정보를 참조 하십시오. [연결 문자열 Reference](https://www.connectionstrings.com/)합니다. 이 다른 공급 업체 사이트 샘플 연결 문자열 및 데이터 공급자에 대 한 자세한 내용 및 필요한 연결 정보를 포함 합니다.

## <a name="whats-next"></a>다음 단계  
 데이터 원본 및 연결하는 방법에 대한 정보를 제공한 후 다음 페이지는 **대상 선택**입니다. 이 페이지에서는 데이터 대상 및 연결하는 방법에 대한 정보를 제공합니다. 자세한 내용은 [대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)을 참조하세요.
 
## <a name="see-also"></a>참고 항목
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)




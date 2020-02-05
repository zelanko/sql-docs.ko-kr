---
title: Excel 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 82e21333bdd0f4be27f19ee19f43fd5f0abab309
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71285572"
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Excel 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 아티클에서는 SQL Server 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **Microsoft Excel** 데이터 원본에 연결하는 방법을 보여 줍니다.

다음 스크린샷은 Microsoft Excel 통합 문서에 대한 샘플 연결을 보여 줍니다.

![Excel 연결](../../integration-services/import-export-data/media/excel-connection.png) 

Excel 파일에 연결하려면 추가 파일을 다운로드하여 설치해야 할 수도 있습니다. 자세한 내용은 [Excel에 연결하는 데 필요한 파일 가져오기](../load-data-to-from-excel-with-ssis.md#files-you-need)를 참조하세요.

> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.

## <a name="options-to-specify"></a>지정할 옵션

> [!NOTE]
> 이 데이터 공급자에 대한 연결 옵션은 Excel이 원본 또는 대상인지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

**Excel 파일 경로**  
 Excel 파일의 경로와 파일 이름을 지정합니다. 다음은 그 예입니다.
-   로컬 컴퓨터의 파일은 **C:\\MyData.xlsx**입니다.
-   네트워크 공유의 파일은 **\\\\Sales\\Database\\Northwind.xlsx**입니다.

또는 **찾아보기**를 클릭합니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 스프레드시트를 찾습니다.  

> [!NOTE]
> 마법사에서는 암호로 보호된 Excel 파일을 열 수 없습니다.

 **Excel 버전**  
원본 또는 대상 통합 문서에서 사용할 Excel 버전을 선택합니다.

**첫 행은 열 이름으로**  
데이터의 첫 번째 행에 열 이름이 포함되는지 여부를 나타냅니다.
-   데이터에 열 이름이 포함되어 있지 않은데 이 옵션을 사용하도록 설정하는 경우 마법사는 원본 데이터의 첫 번째 행을 열 이름으로 간주합니다.
-   데이터에 열 이름이 포함되어 있지만 이 옵션을 사용하지 않도록 설정하는 경우 마법사는 열 이름 행을 첫 번째 데이터 행으로 간주합니다.

데이터에 열 이름이 포함되지 않는 것으로 지정하면 마법사는 F1, F2 등을 열 머리글로 사용합니다.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Excel이 표시되지 않는 데이터 원본 목록
데이터 원본 목록에 Excel이 표시되지 않는 경우 64비트 마법사를 실행하고 있는지 확인합니다. Excel 및 Access 공급자는 일반적으로 32비트이므로 64비트 마법사에는 표시되지 않습니다. 이 경우 32비트 마법사를 대신 실행합니다.

> [!NOTE]
> 64비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용하려면 SQL Server를 설치해야 합니다. SSDT(SQL Server Data Tools) 및 SSMS(SQL Server Management Studio)는 32비트 애플리케이션이며, 32비트 버전의 마법사를 포함하여 32비트 파일만 설치합니다.

## <a name="see-also"></a>참고 항목
[SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](../load-data-to-from-excel-with-ssis.md)  
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


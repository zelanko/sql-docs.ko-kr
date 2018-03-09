---
title: "Excel 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 16ace15a73d9ef727612c59f8c9329a4d4437312
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Excel 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사)
이 항목에서는 SQL Server 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **Microsoft Excel** 데이터 원본에 연결하는 방법을 보여 줍니다.

다음 스크린샷은 Microsoft Excel 통합 문서에 대한 샘플 연결을 보여 줍니다.

![Excel 연결](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>지정할 옵션

> [!NOTE]
> 이 데이터 공급자에 대한 연결 옵션은 Excel이 원본 또는 대상인지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

**Excel 파일 경로**  
 Excel 파일의 경로와 파일 이름을 지정합니다. 예를 들어 다음과 같이 사용할 수 있습니다.
-   로컬 컴퓨터의 파일은 **C:\\MyData.xlsx**입니다.
-   네트워크 공유의 파일은 **\\\\Sales\\Database\\Northwind.xlsx**입니다.

또는 **찾아보기**를 클릭합니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 스프레드시트를 찾습니다.  

> [!NOTE]
> 마법사에서는 암호로 보호된 Excel 파일을 열 수 없습니다.

 **Excel 버전**  
원본 통합 문서에서 사용할 Excel 버전을 선택합니다.

> [!IMPORTANT]
> Excel 파일에 연결하려면 추가 파일을 다운로드하여 설치해야 할 수도 있습니다. 자세한 내용은 이 페이지의 [Excel에 연결하는 데 필요한 파일 가져오기](#officeDownloads)를 참조하세요.

**첫 행은 열 이름으로**  
데이터의 첫 번째 행에 열 이름이 포함되는지 여부를 나타냅니다.
-   데이터에 열 이름이 포함되어 있지 않은데 이 옵션을 사용하도록 설정하는 경우 마법사는 원본 데이터의 첫 번째 행을 열 이름으로 간주합니다.
-   데이터에 열 이름이 포함되어 있지만 이 옵션을 사용하지 않도록 설정하는 경우 마법사는 열 이름 행을 첫 번째 데이터 행으로 간주합니다.

데이터에 열 이름이 포함되지 않는 것으로 지정하면 마법사는 F1, F2 등을 열 머리글로 사용합니다.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Excel이 표시되지 않는 데이터 원본 목록
데이터 원본 목록에 Excel이 표시되지 않는 경우 64비트 마법사를 실행하고 있는지 확인합니다. Excel 및 Access 공급자는 일반적으로 32비트이므로 64비트 마법사에는 표시되지 않습니다. 이 경우 32비트 마법사를 대신 실행합니다.

> [!NOTE]
> 64비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용하려면 SQL Server를 설치해야 합니다. SSDT(SQL Server Data Tools) 및 SSMS(SQL Server Management Studio)는 32비트 응용 프로그램이며, 32비트 버전의 마법사를 포함하여 32비트 파일만 설치합니다.

## <a name="officeDownloads"></a> Excel에 연결하는 데 필요한 파일 가져오기  
Excel 및 Access를 포함하여 Microsoft Office 데이터 원본용 연결 구성 요소가 아직 설치되지 않은 경우 해당 구성 요소를 다운로드해야 할 수 있습니다. [Microsoft Access 데이터베이스 엔진 2016 재배포 가능](https://www.microsoft.com/download/details.aspx?id=54920)에서 최신 버전의 Excel 및 Access 파일용 연결 구성 요소를 다운로드합니다.
  
최신 버전 구성 요소는 이전 버전의 Excel에서 만든 파일을 열 수 있습니다.

컴퓨터에 32비트 버전의 Office가 설치되어 있으면 32비트 버전 구성 요소를 설치해야 하며 패키지도 32비트 모드에서 실행해야 합니다.

Office 365 구독이 있는 경우 Microsoft Access 2016 런타임이 아닌 Access 데이터베이스 엔진 2016 재배포 가능 패키지를 다운로드해야 합니다. 설치 관리자를 실행하는 경우 Office 간편 실행 구성 요소와 함께 다운로드를 설치할 수 없다는 오류 메시지가 표시될 수 있습니다. 이 오류 메시지를 무시하려면 명령 프롬프트 창을 열고 `/quiet` 스위치를 통해 다운로드한 .EXE 파일을 실행하여 자동 모드에서 설치를 실행합니다. 예를 들어 다음과 같이 사용할 수 있습니다.

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>관련 항목:
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


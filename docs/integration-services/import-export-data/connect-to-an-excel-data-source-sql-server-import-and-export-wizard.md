---
title: "Excel 데이터 원본 (SQL Server 가져오기 및 내보내기 마법사)에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b4411fdd2337d93f15b149febf845fb7b0762c40
ms.contentlocale: ko-kr
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Excel 데이터 원본 (SQL Server 가져오기 및 내보내기 마법사)에 연결
이 항목에 연결 하는 방법을 보여 줍니다.는 **Microsoft Excel** 에서 데이터 소스는 **데이터 원본을 선택** 또는 **대상 선택** SQL Server 가져오기 및 내보내기 마법사의 페이지입니다.

다음 스크린샷은 Microsoft Excel 통합 문서에 대한 샘플 연결을 보여 줍니다.

![Excel 연결](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>지정 하는 옵션

> [!NOTE]
> 이 데이터 공급자에 대 한 연결 옵션은 Excel 소스 또는 대상 인지는 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

**Excel 파일 경로**  
 Excel 파일에 대 한 경로 파일 이름을 지정 합니다. 예를 들어
-   로컬 컴퓨터에 있는 파일에 대 한 **c:\\MyData.xlsx**합니다.
-   네트워크 공유에서 파일에 대 한  **\\ \\Sales\\데이터베이스\\Northwind.xlsx**합니다.

또는 **찾아보기**를 클릭합니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 스프레드시트를 찾습니다.  

> [!NOTE]
> 마법사에서는 암호로 보호된 Excel 파일을 열 수 없습니다.

 **Excel 버전**  
원본 통합 문서에서 사용할 Excel 버전을 선택합니다.

> [!IMPORTANT]
> Excel 파일에 연결 하는 추가 파일 다운로드 및 설치를 할 수 있습니다. 참조 [Excel에 연결 하는 데 필요한 파일 가져오기](#officeDownloads) 자세한 내용을 보려면이 페이지에 있습니다.

**첫 행은 열 이름으로**  
데이터의 첫 번째 행에 열 이름을 포함할지 여부를 나타냅니다.
-   데이터 열 이름 없는 표시 되지만이 옵션을 사용 하는 경우 마법사는 열 이름으로 원본 데이터의 첫 번째 행을 처리 합니다.
-   데이터 열 이름을 포함 하는 경우이 옵션을 사용 하지 않도록 설정 마법사는 열 이름이 행 데이터의 첫 번째 행으로 처리 합니다.

데이터 열 이름 없는 있는지를 지정 하면 마법사 F1, F2 등 열 머리글로 사용 합니다.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Excel 데이터 원본 목록에 표시 되지 않습니다.
Excel 데이터 원본의 목록에 표시 되지 않으면, 하는 경우 64 비트 마법사 실행은 무엇입니까? Excel 및 Access에 대 한 공급자는 일반적으로 32 비트 및 64 비트 마법사에 표시 되지 않습니다. 대신 32 비트 마법사를 실행 합니다.

> [!NOTE]
> 64 비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용 하려면 SQL Server를 설치 해야 합니다. SQL Server Data Tools (SSDT) 및 SQL Server Management Studio (SSMS)는 32 비트 응용 프로그램 및 32 비트 버전의 마법사를 포함 하 여 32 비트 파일을 설치 합니다.

## <a name="officeDownloads"></a>Excel에 연결 하는 데 필요한 파일 가져오기  
설치 되어 있지 않으면 Excel 및 Access을 비롯 한 Microsoft Office 데이터 원본에 대 한 연결 구성 요소를 다운로드 해야 할 수 있습니다. 최신 버전의 Excel 및 Access 모두 파일에 여기에 대 한 연결 구성 요소 다운로드: [Microsoft Access 데이터베이스 엔진 2016 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=54920)합니다.
  
최신 버전의 구성 요소는 이전 버전의 Excel에서 만든 파일을 열 수 있습니다.

컴퓨터에 32 비트 버전의 Office가 32 비트 버전의 구성 요소를 설치 해야 합니다 및 32 비트 모드로 패키지를 실행 해야 합니다.

Office 365 구독을 보유 하는 경우 Access 데이터베이스 엔진 2016 재배포 가능 패키지 및 Microsoft Access 2016 런타임이 아닌를 다운로드 해야 합니다. 설치 관리자를 실행 하는 경우 Office 간편 실행 구성 요소와는 다운로드-함께 설치할 수 없습니다 오류 메시지가 표시 될 수 있습니다. 이 오류 메시지를 무시 하려면 설치 자동 모드로 명령 프롬프트 창을 열고 실행 하 여 실행 된 합니다. 와 함께 다운로드 한 EXE 파일의 `/quiet` 전환 합니다. 예를 들어

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



---
title: Access 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 87efb901b3bdf01140db90b3aa2ee0d72d2ae67a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Access 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사)
이 항목에서는 SQL Server 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **Microsoft Access** 데이터 원본에 연결하는 방법을 보여 줍니다.

다음 스크린샷은 Microsoft Access 데이터베이스에 대한 샘플 연결을 보여 줍니다. 이 예제에서는 대상 데이터베이스에서 작업 그룹 정보 파일을 사용하지 않으므로 사용자 이름과 암호를 입력할 필요가 없습니다.

![Access에 연결](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>지정할 옵션

> [!NOTE]
> 이 데이터 공급자에 대한 연결 옵션은 Access가 원본 또는 대상인지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

**데이터 원본**  
데이터 공급자 목록에는 Microsoft Access에 대한 여러 항목이 포함될 수 있습니다. 최근에 설치된 버전 또는 데이터베이스 파일을 만든 Access 버전에 해당하는 버전을 선택합니다.

|데이터 원본|Office 버전|
|-------|-------|
|Microsoft Access(Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access(Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access(Microsoft Access 데이터베이스 엔진)|Office 2010 및 Office 2007|
|Microsoft Access(Microsoft Jet 데이터베이스 엔진)|Office 2007 이전 버전|

> [!IMPORTANT]
> Access 데이터베이스에 연결하려면 추가 파일을 다운로드하여 설치해야 할 수 있습니다. 자세한 내용은 이 페이지의 [Access에 연결하는 데 필요한 파일 가져오기](#officeDownloads)를 참조하세요.

 **파일 이름**  
Access 파일의 경로와 파일 이름을 지정합니다. 예를 들어 로컬 컴퓨터에 있는 파일에 대해서는 **C:\\MyData.mdb**, 네트워크 공유에 있는 파일에 대해서는 **\\\\Sales\\Database\\Northwind.mdb**로 지정합니다. 또는 **찾아보기**를 클릭합니다. 

 >   [!NOTE] 
 > **찾아보기**를 클릭하여 Access 파일을 찾는 경우 **열기** 대화 상자에서 기본적으로 이전 .MDB 형식 및 파일 확장명이 포함된 파일을 필터링합니다. 그러나 데이터 공급자는 최신 .ACCDB 형식 및 파일 확장명이 포함된 파일을 열 수도 있습니다.
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 데이터베이스 파일을 찾습니다.  
  
 **User name**  
작업 그룹 정보 파일이 데이터베이스에 연결되는 경우 유효한 사용자 이름을 제공합니다.  
  
 **암호**  
작업 그룹 정보 파일이 데이터베이스에 연결되는 경우 여기에 사용자의 암호를 제공합니다.
 
데이터베이스가 모든 사용자에 대해 단일 암호로 보호되는 경우 [암호로 보호된 데이터베이스 파일인가요?](#database_password)를 참조하세요.
  
 **고급**  
**데이터 연결 속성** 대화 상자에서 데이터베이스 암호 또는 기본이 아닌 작업 그룹 정보 파일과 같은 고급 옵션을 지정합니다.  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>Access가 표시되지 않는 데이터 원본 목록
데이터 원본 목록에 Access가 표시되지 않는 경우 64비트 마법사를 실행하고 있나요? Excel 및 Access 공급자는 일반적으로 32비트이므로 64비트 마법사에는 표시되지 않습니다. 이 경우 32비트 마법사를 대신 실행합니다.

> [!NOTE]
> 64비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용하려면 SQL Server를 설치해야 합니다. SSDT(SQL Server Data Tools) 및 SSMS(SQL Server Management Studio)는 32비트 응용 프로그램이며, 32비트 버전의 마법사를 포함하여 32비트 파일만 설치합니다.

## <a name="officeDownloads"></a> Access에 연결하는 데 필요한 파일 가져오기  
Excel 및 Access를 포함하여 Microsoft Office 데이터 원본용 연결 구성 요소가 아직 설치되지 않은 경우 해당 구성 요소를 다운로드해야 할 수 있습니다. [Microsoft Access 데이터베이스 엔진 2016 재배포 가능 구성 요소](https://www.microsoft.com/download/details.aspx?id=54920)에서 최신 버전의 Access 및 Excel 파일용 연결 구성 요소를 다운로드합니다.
  
최신 버전의 구성 요소는 이전 버전의 Access에서 만든 파일을 열 수 있습니다.

컴퓨터에 32비트 버전의 Office가 있는 경우 32비트 버전의 구성 요소를 설치해야 하며, 패키지도 32비트 모드에서 실행해야 합니다.

Office 365 구독이 있는 경우 Microsoft Access 2016 런타임이 아닌 Access 데이터베이스 엔진 2016 재배포 가능 패키지를 다운로드해야 합니다. 설치 관리자를 실행하는 경우 Office 간편 실행 구성 요소와 함께 다운로드를 설치할 수 없다는 오류 메시지가 표시될 수 있습니다. 이 오류 메시지를 무시하려면 명령 프롬프트 창을 열고 `/quiet` 스위치를 통해 다운로드한 .EXE 파일을 실행하여 자동 모드에서 설치를 실행합니다. 예를 들어 다음과 같이 사용할 수 있습니다.

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a> 암호로 보호된 데이터베이스 파일인가요?
Access 데이터베이스가 암호로 보호되지만 작업 그룹 정보 파일이 사용되지 않는 경우도 있습니다. 모든 사용자가 동일한 암호를 제공해야 하지만, 사용자 이름은 입력할 필요가 없습니다. 데이터베이스 암호를 제공하려면 다음을 수행합니다.

1.  **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **고급** 단추를 클릭하여 **데이터 연결 속성** 대화 상자를 엽니다.  
2.  **데이터 연결 속성** 대화 상자에서 **모두** 탭을 선택합니다.  
3.  속성 및 값 목록에서 **Jet OLEDB:Database Password**를 선택합니다.   
    
    ![액세스 암호 지정 - 화면 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  **값 편집**을 클릭하여 **속성 값 편집** 대화 상자를 엽니다.  
    
    ![액세스 암호 지정 - 화면 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  **속성 값 편집** 대화 상자에서 데이터베이스 암호를 입력합니다.
6.  각 대화 상자에서 **확인**을 클릭하여 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지로 돌아가서 계속합니다.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Access에서 내보낼 때 일련 번호 값 유지
원본 데이터의 기존 ID 값을 대상 테이블의 ID 열에 삽입할 수 있게 하려면 **열 매핑** 대화 상자에서 **ID 삽입 가능** 옵션을 선택합니다. 기본적으로 대상 ID 열에는 일반적으로 기존 값을 삽입할 수 없습니다. **열 매핑** 대화 상자를 표시하려면 마법사의 **원본 테이블 및 뷰 선택** 페이지에 도달할 때 **매핑 편집**을 선택합니다. 이러한 페이지를 살펴보려면 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 및 [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)을 참조하세요.

기존 기본 키가 ID 열, 자동 번호 열에 있는 경우 기존 기본 키 값을 유지하려면 일반적으로 이 옵션을 선택해야 합니다. 그러지 않으면 대상 ID 열은 일반적으로 새 값을 할당합니다.

## <a name="see-also"></a>관련 항목:
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


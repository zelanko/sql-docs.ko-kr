---
title: "(SQL Server 가져오기 및 내보내기 마법사)는 Access 데이터 소스에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2a5deb6e6ec95e6f6707abe9ad85374b2334e05
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>(SQL Server 가져오기 및 내보내기 마법사)는 Access 데이터 소스에 연결
이 항목에 연결 하는 방법을 보여 줍니다.는 **Microsoft Access** 에서 데이터 소스는 **데이터 원본을 선택** 또는 **대상 선택** SQL Server 가져오기 및 내보내기 마법사의 페이지입니다.

다음 스크린샷은 Microsoft Access 데이터베이스에 대한 샘플 연결을 보여 줍니다. 이 예제에서는 필요가 사용자 이름 및 암호를 입력 대상 데이터베이스는 작업 그룹 정보 파일을 사용 하지 않아 합니다.

![Access에 연결](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>지정 하는 옵션

> [!NOTE]
> 이 데이터 공급자에 대 한 연결 옵션 액세스 소스 또는 대상 인지 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

**데이터 원본**  
데이터 공급자의 목록은 Microsoft Access에 대 한 여러 항목을 포함할 수 있습니다. 최근에 설치 된 버전 또는 데이터베이스 파일을 만든 Access의 버전에 해당 하는 버전을 선택 합니다.

|데이터 원본|Office 버전|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (Microsoft Access 데이터베이스 엔진)|Office 2010 및 Office 2007|
|Microsoft Access (Microsoft Jet 데이터베이스 엔진)|Office 2007 이전에 지정 된 office 버전|

> [!IMPORTANT]
> 선택 하는 액세스의 버전에 연결 하는 데 추가 파일 다운로드 및 설치를 할 수 있습니다. 참조 [Access에 연결 하는 데 필요한 파일을 가져올](#officeDownloads) 자세한 내용을 보려면이 페이지에 있습니다.

버전을 지정 하는 경우 문제가 있는 경우 다른 버전으로 이전 버전을 지정 하십시오. 예를 들어 수 Microsoft Office 365 구독을 보유 하기 때문에 Office 2016 데이터 공급자를 설치할 수 없습니다. 액세스 2016 및 Excel 2016에 대 한 데이터 공급자의 Microsoft Office 데스크톱 버전으로 설치할 수 있습니다. 이 경우 Access 2013 액세스 2016 대신 지정할 수 있습니다. 두 버전의 공급자는 기능적으로 동일 합니다. 에 지정 된 Office 2016 런타임의 이러한 제한을 [이 블로그 게시물](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/)합니다.

 **파일 이름**  
Access 파일에 대 한 경로 파일 이름을 지정 합니다. 예를 들어 **c:\\MyData.mdb** 로컬 컴퓨터에서 파일 또는  **\\ \\Sales\\데이터베이스\\Northwind.mdb** 네트워크 공유에 파일에 대 한 합니다. 또는 **찾아보기**를 클릭합니다. 

 >   [!NOTE] 
 > 클릭 하면 **찾아보기** Access 파일을 찾은 **열려** 이전를 사용 하 여 파일에 대 한 대화 상자 필터입니다. 기본적으로 MDB 형식 및 파일 확장명입니다. 그러나 데이터 공급자 최신 형식으로 파일을 열 수도 있습니다. ACCDB 형식 및 파일 확장명입니다.
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 데이터베이스 파일을 찾습니다.  
  
 **사용자 이름**  
작업 그룹 정보 파일을 데이터베이스에 연결 된 경우에 유효한 사용자 이름을 제공 합니다.  
  
 **암호**  
작업 그룹 정보 파일을 데이터베이스에 연결 된 경우 여기에 사용자의 암호를 제공 합니다.
 
데이터베이스가 모든 사용자에 대해 단일 암호로 보호 되 면 참조 [암호로 보호 된 데이터베이스 파일은?](#database_password)합니다.
  
 **고급**  
데이터베이스 암호나 기본이 아닌 작업 그룹 정보 파일과 같은 고급 옵션을 지정 된 **데이터 연결 속성** 대화 상자.  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>Access 데이터 원본 목록에 표시 되지 않는
액세스 보이지 않으면 데이터 원본 목록에서 64 비트 마법사 실행은 무엇입니까? Excel 및 Access에 대 한 공급자는 일반적으로 32 비트 및 64 비트 마법사에 표시 되지 않습니다. 대신 32 비트 마법사를 실행 합니다.
  
## <a name="officeDownloads"></a>에 액세스 하려면 연결 하는 데 필요한 파일 가져오기  
설치 되어 있지 않으면 Excel 및 Access을 비롯 한 Microsoft Office 데이터 원본에 대 한 연결 구성 요소를 다운로드 해야 할 수 있습니다.

최신 버전 구성 요소는 이전 버전의 프로그램에서 만든 파일을 열 수 있습니다. 대부분의 경우에서 이전 버전의 구성 요소 프로그램의 이후 버전에서 만든 파일을 열 수도 있습니다. 예를 들어 Office 2016 구성 요소를 설치할 수 없는 경우 Office 2013 구성 요소 대신 사용 합니다. 두 버전의 공급자는 기능적으로 동일 합니다. 에 지정 된 Office 2016 런타임의 이러한 제한을 [이 블로그 게시물](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/)합니다.

이 64 비트 컴퓨터-에서도 일반적인-컴퓨터에 32 비트 버전의 Office 32 비트 버전의 구성 요소를 설치 해야 합니다. 32 비트 마법사를 실행 하거나 32 비트 모드에서 마법사에서 생성 하는 SQL Server Integration Services 패키지를 실행 해야 할 수도 있습니다.

|Microsoft Office 버전|다운로드|  
|------------------------------|--------------|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2007|[2007 Office System 드라이버: 데이터 연결 구성 요소](https://www.microsoft.com/download/details.aspx?id=23734)|    

## <a name="database_password"></a>암호로 보호 된 데이터베이스 파일 인가요?
경우에 따라 Access 데이터베이스는 암호로 보호 되어 있지만 작업 그룹 정보 파일을 사용 하 여 되지 않습니다. 모든 사용자가 같은 암호를 제공 해야 하지만 사용자 이름을 입력할 필요가 없습니다. 데이터베이스 암호를 제공 하려면 다음을 수행 합니다.

1.  에 **데이터 원본을 선택** 또는 **대상 선택** 페이지는 **고급** 버튼을 클릭은 **데이터 연결 속성** 대화 상자.  
2.  에 **데이터 연결 속성** 대화 상자는 **모든** 탭 합니다.  
3.  속성 및 값의 목록에서 선택 **Jet OLEDB:Database 암호**합니다.   
    
    ![화면 1 액세스 암호를 지정 합니다.](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  클릭 **값 편집** 열려는 **속성 값 편집** 대화 상자.  
    
    ![화면 2 액세스 암호를 지정 합니다.](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  에 **속성 값 편집** 대화 상자에서 데이터베이스 암호를 입력 합니다.
6.  클릭 **확인** 돌아가려면 각 대화 상자에는 **데이터 원본을 선택** 또는 **대상 선택** 마법사의 페이지 하 고 계속 합니다.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Access에서 내보낼 때 일련 번호 값을 유지 합니다.
대상 테이블에 id 열에 삽입 될 원본 데이터의 기존 id 값을 허용 하려면 선택은 **id 삽입 가능** 옵션에 **열 매핑** 대화 상자. 기본적으로 대상 id 열 일반적으로 하지 않는 수 있도록 기존 값을 삽입 합니다. 표시는 **열 매핑** 대화 상자에서 **매핑을 편집 합니다.** 나타나면는 **원본 테이블 및 뷰 선택** 마법사의 페이지입니다. 이러한 페이지를 살펴보고 참조 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 및 [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)합니다.

기존 기본 키가 ID 열, 자동 번호 열에 있는 경우 기존 기본 키 값을 유지하려면 일반적으로 이 옵션을 선택해야 합니다. 그러지 않으면 대상 ID 열은 일반적으로 새 값을 할당합니다.

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



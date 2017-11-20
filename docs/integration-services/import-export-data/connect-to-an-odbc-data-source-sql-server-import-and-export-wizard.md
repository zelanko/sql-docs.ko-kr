---
title: "ODBC 데이터 원본 (SQL Server 가져오기 및 내보내기 마법사)에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 0e3ffe2ff1695de69be7149f4be7b42f57b0e991
ms.contentlocale: ko-kr
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>ODBC 데이터 원본 (SQL Server 가져오기 및 내보내기 마법사)에 연결
이 항목에 연결 하는 방법을 보여 줍니다.는 **ODBC** 에서 데이터 소스는 **데이터 원본을 선택** 또는 **대상 선택** SQL Server 가져오기 및 내보내기 마법사의 페이지입니다.

Microsoft에서 필요한 또는 제 3 자에서 ODBC 드라이버를 다운로드 해야 할 수 있습니다.

제공 해야 하는 필요한 연결 정보를 조회 할 수 있습니다. 이 다른 공급 업체 사이트- [연결 문자열 Reference](https://www.connectionstrings.com/) -샘플 연결 문자열 및 데이터 공급자에 대 한 자세한 내용 및 필요한 연결 정보를 포함 합니다.

## <a name="make-sure-the-driver-you-want-is-installed"></a>설치 된 드라이버를 있는지 확인
1.  에 대 한 검색 하거나 찾아볼는 **ODBC 데이터 원본 (64 비트)** 제어판에서 애플릿을 합니다. 에 대 한 검색 하거나 찾아볼 있음을 알고 있는 32 비트 드라이버를 사용 하는 32 비트 드라이버 하기만 하면, **ODBC 데이터 원본 (32 비트)** 대신 합니다.
2.  애플릿을 시작 합니다. **ODBC 데이터 원본 관리자** 창이 열립니다.
3.  에 **드라이버** 탭을 컴퓨터에 설치 된 모든 ODBC 드라이버의 목록을 찾을 수 있습니다. (드라이버 중 일부의 이름은 여러 언어에 나타날 수 있습니다.)

    에 설치 된 64 비트 드라이버 목록의 예를 들면 다음과 같습니다.

    ![설치 된 64 비트 ODBC 드라이버](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> 드라이버의 설치 및 64 비트 애플릿에서 표시 되지 않으면 있는지 알고 있는 경우 대신 32 비트 애플릿에서 찾습니다. 또한 인지 64 비트 또는 32 비트 SQL Server 가져오기 및 내보내기 마법사를 실행 해야 하는지 여부.
>
> 64 비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용 하려면 SQL Server를 설치 해야 합니다. SQL Server Data Tools (SSDT) 및 SQL Server Management Studio (SSMS)는 32 비트 응용 프로그램 및 32 비트 버전의 마법사를 포함 하 여 32 비트 파일을 설치 합니다.
    
## <a name="step-1---select-the-data-source"></a>1 단계-데이터 소스를 선택 합니다.
컴퓨터에 설치 된 ODBC 드라이버는 데이터 원본의 드롭 다운 목록에 나열 되지 않습니다. ODBC 드라이버를 연결 하려면 선택 하 여 시작 된 **.NET Framework Data Provider for ODBC** 데이터 원본으로 **데이터 원본을 선택** 또는 **대상 선택** 마법사의 페이지입니다. 이 공급자는 ODBC 드라이버 주위에서 래퍼로 역할을 합니다.

다음은.NET Framework Data Provider for ODBC 선택한 후 볼 수 있는 제네릭 화면입니다.

![전에 odbc SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>2 단계-연결 정보를 제공 합니다.
다음 단계에서는 ODBC 드라이버와 데이터 원본에 대 한 연결 정보를 제공 하는 것입니다. 두 가지 옵션이 있습니다.
1.  제공 된 **DSN** (데이터 원본 이름) 이미 존재 하지 않거나 사용 하 여 만든는 **ODBC 데이터 원본 관리자** 제어판에서 애플릿을 합니다. DSN은 ODBC 데이터 원본에 연결 하는 데 필요한 설정의 저장 된 컬렉션입니다.

    DSN 이름을 이미 모르거나 지금 새 DSN을 작성 하는 방법을 알고 있는 경우이 페이지의 나머지 부분을 건너뛸 수 있습니다. DSN에 이름을 입력는 **Dsn** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지, 다음 마법사의 다음 단계를 계속 합니다.

    [DSN을 제공 합니다.](#odbc_dsn)
    
2.  제공 된 **연결 문자열**, 수 있는 온라인 상태를 조회 하거나 만들 사용 하 여 컴퓨터에서 테스트는 **ODBC 데이터 원본 관리자** 애플릿을 합니다.

    연결 문자열이 이미 했거나을 만드는 방법을 알고 있는 경우이 페이지의 나머지 부분을 건너뛸 수 있습니다. 에 대 한 연결 문자열을 입력에서 **ConnectionString** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지, 다음 마법사의 다음 단계를 계속 합니다.

    [연결 문자열을 제공](#odbc_connstring)

연결 문자열을 제공 하는 경우는 **데이터 원본을 선택** 또는 **대상 선택** 페이지 마법사, 서버 및 데이터베이스 이름 및 인증 방법 같은 데이터 원본에 연결 하는 데 사용 하려는 모든 연결 정보를 표시 합니다. DSN을 제공 하면이 정보는 표시 되지 않습니다.

## <a name="odbc_dsn"></a>옵션 1-사용자 DSN을 제공 합니다.
DSN (데이터 원본 이름) 사용 하 여 연결 정보를 제공 하려는 경우 사용 하 여는 **ODBC 데이터 원본 관리자** 애플릿을 기존 DSN의 이름을 찾으려면 또는 새 DSN을 만들려고 합니다.
1.  에 대 한 검색 하거나 찾아볼는 **ODBC 데이터 원본 (64 비트)** 제어판에서 애플릿을 합니다. 32 비트 드라이버만 했거나 32 비트 드라이버를 사용 해야 할 경우에 대 한 검색 하거나 찾아볼 **ODBC 데이터 원본 (32 비트)** 대신 합니다.
2.  애플릿을 시작 합니다. **ODBC 데이터 원본 관리자** 창이 열립니다. 다음은 애플릿을 표시 되는 모양입니다.

    ![ODBC 관리자 제어판 애플릿](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  하려면 **기존의 DSN을 사용 하 여** 데이터 원본의 경우에 표시 되는 DSN을 사용할 수 있습니다는 **사용자 DSN**, **시스템 DSN**, 또는 **파일 DSN** 탭 합니다. 이름을 확인 한 다음 마법사 돌아가서에 입력 된 **Dsn** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 이 페이지의 나머지 부분을 건너뛰고 마법사의 다음 단계를 계속 합니다.
4.  하려면 **새 DSN 만들기**표시 되도록 할지 여부를 있습니다 (사용자 DSN)는 컴퓨터의 모든 사용자에 게 표시에 포함 하 여 Windows 서비스 (시스템 DSN), 결정, 또는 파일 DSN () 파일에 저장 합니다. 이 예에서는 새 시스템 DSN을 만듭니다.
5. 에 **시스템 DSN** 탭을 클릭 **추가**합니다.

    ![새 ODBC 시스템 DSN 추가](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  에 **새 데이터 원본을 만들** 대화 상자, 데이터 원본에 대 한 드라이버를 선택한 다음 클릭 **마침**합니다.

    ![새 시스템 DSN에 대 한 드라이버를 선택 합니다.](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. 드라이버는 이제 데이터 원본에 연결 하는 데 필요한 정보를 입력할 수 있는 하나 이상의 드라이버 관련 화면을 표시 합니다. (SQL Server 드라이버에 대 한 예를 들어 있는 경우 사용자 지정 설정의 4 페이지) 를 완료 한 후 DSN 새 시스템 목록에 나타납니다.

    ![목록에서 새 시스템 DSN](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  마법사를 다시 이동 하 고 DSN에 이름을 입력는 **Dsn** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 마법사의 다음 단계를 계속 합니다.

## <a name="odbc_connstring"></a>옵션 2-연결 문자열을 제공
연결 문자열을 사용 하 여 연결 정보를 제공 하려는 경우이 항목의 나머지 부분에서는 연결 문자열이 필요 합니다.

이 예제에서는 Microsoft SQL Server에 연결 하는 다음 연결 문자열을 사용 하려고 합니다.

    ```
    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
    ```

에 대 한 연결 문자열을 입력에서 **ConnectionString** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 페이지. 연결 문자열을 입력 한 후 마법사는 문자열을 구문 분석 하 고 목록에서 개별 속성 및 해당 값을 표시 합니다.

다음은 연결 문자열을 입력 한 후 표시 되는 화면입니다.

![다음 odbc SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> ODBC 드라이버에 대 한 연결 옵션 여부 소스 또는 대상 사용자를 구성 하는 동일 합니다. 즉, 표시 되는 옵션은 둘 다에 동일한는 **데이터 원본을 선택** 및 **대상 선택** 마법사의 페이지입니다.

## <a name="get-the-connection-string-online"></a>연결 문자열을 온라인 가져옵니다.
온라인 ODBC 드라이버에 대 한 연결 문자열을 찾으려고 참조 [연결 문자열 Reference](https://www.connectionstrings.com/)합니다. 이 다른 공급 업체 사이트 샘플 연결 문자열 및 데이터 공급자에 대 한 자세한 내용 및 필요한 연결 정보를 포함 합니다.

## <a name="get-the-connection-string-with-an-app"></a>연결 문자열을 앱과 가져옵니다.
작성 하 고 테스트해 사용자 컴퓨터에서 ODBC 드라이버에 대 한 연결 문자열을 사용할 수 있습니다는 **ODBC 데이터 원본 관리자** 제어판에서 애플릿을 합니다. 사용자의 연결에 대 한 파일 DSN을 만들려면 다음 연결 문자열을 조합할 파일 DSN에서 설정을 복사 합니다. 이 여러 단계가 필요 하지만 유효한 연결 문자열을 지정 했는지 확인 하는 데 도움이 됩니다.

1.  에 대 한 검색 하거나 찾아볼는 **ODBC 데이터 원본 (64 비트)** 제어판에서 애플릿을 합니다. 32 비트 드라이버만 했거나 32 비트 드라이버를 사용 해야 할 경우에 대 한 검색 하거나 찾아볼 **ODBC 데이터 원본 (32 비트)** 대신 합니다.
2.  애플릿을 시작 합니다. **ODBC 데이터 원본 관리자** 창이 열립니다.
3.  이제는 **파일 DSN** 애플릿 탭 합니다. **추가**를 클릭합니다.

    이 예제에 대 한 연결 문자열에 필요한 특정 형식에는 이름-값 쌍을 저장 하는 파일 DSN 하므로 파일 DSN 보다는 사용자 DSN 또는 시스템 DSN를 만듭니다.

    ![새 ODBC 파일 DSN을 추가 합니다.](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  에 **새 데이터 원본 만들기** 대화 상자, 목록에서 드라이버를 선택 하 고 클릭 **다음**합니다. 이 예제는 Microsoft SQL Server에 연결 하는 데 필요한 연결 문자열 인수를 포함 하는 DSN을 만드는 것입니다.

    ![새 ODBC 데이터 원본 만들기](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  위치를 선택 하 고 새 파일 DSN에 대 한 파일 이름을 입력 한 다음 클릭 **다음**합니다. 찾아 이후 단계에서 열 수 있도록 파일을 저장할 위치를 기억 합니다.

    ![새 파일 DSN을 저장 합니다.](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  선택 항목을 요약을 검토 한 다음 클릭 **마침**합니다.

7.  클릭 한 후 **마침**, 선택한 드라이버 하나 이상의 소유 화면 연결 하는 데 필요한 정보를 가져오지를 표시 합니다. 일반적으로이 정보는 서버, 로그인 정보 및 서버 기반 데이터 원본 및 파일, 형식 및 파일 기반 데이터 원본에 대 한 버전에 대 한 데이터베이스를 포함 합니다.

8. 데이터 원본을 구성 하 고를 클릭 한 후 **마침**, 일반적으로 선택한 항목의 요약을 볼 하 고 테스트할 수 있습니다.

    ![새 파일 DSN 테스트](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. 데이터 원본을 테스트 하 고 대화 상자를 닫습니다 후 파일 DSN 파일 시스템에 저장 한 위치를 찾습니다. 파일 확장명을 변경 하지 않은 경우 기본 확장명은. DSN입니다.

10. 메모장 이나 다른 텍스트 편집기와 저장된 된 파일을 엽니다. 다음은 SQL Server 예제의 내용입니다.

    ```   
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=Microsoft® Windows® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. 복사 하는 이름-값 쌍은 세미콜론으로 구분 하는 연결 문자열에 필요한 값을 붙여 넣습니다.

    샘플 파일 DSN에서에서 필요한 값을 조합, 다음 연결 문자열은 사용할 수 있습니다.
    
        ```
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
        ```

    일반적으로 작동 하는 연결 문자열을 만들려면 ODBC 데이터 원본 관리자가 만든 DSN에 있는 모든 설정 하지 않아도 됩니다.  
    -   항상 ODBC 드라이버를 지정 해야 합니다.
    -   SQL Server와 같은 서버 기반 데이터 원본에 대 한 일반적으로 서버, 데이터베이스 및 로그인 정보를 필요 합니다. 따라서 DSN이 샘플에서는 않아도 TrustServerCertificate, WSID, 또는 응용 프로그램입니다.
    -   파일 기반 데이터 원본에 대 한 이름 및 위치 적어도 파일 필요 합니다.
    
12. 이 연결 문자열을 붙여는 **ConnectionString** 필드에 **데이터 원본을 선택** 또는 **대상 선택** 마법사의 페이지입니다. 마법사는 문자열을 구문 분석 하 고 계속할 준비가 되었습니다.!

    ![다음 odbc SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)




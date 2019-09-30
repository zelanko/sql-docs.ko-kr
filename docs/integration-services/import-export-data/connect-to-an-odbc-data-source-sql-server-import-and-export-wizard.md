---
title: ODBC 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd4dbec9e08b19a0c06c991a7007b449dff02485
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285499"
---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>ODBC 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 항목에서는 SQL Server 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **ODBC** 데이터 원본에 연결하는 방법을 보여 줍니다.

필요한 ODBC 드라이버를 Microsoft 또는 타사에서 다운로드해야 할 수 있습니다.

또한 제공해야 하는 필요한 연결 정보를 찾아야 할 수도 있습니다. 이 타사 사이트([연결 문자열 참조](https://www.connectionstrings.com/))에는 샘플 연결 문자열과 필요한 데이터 공급자 및 연결 정보에 대한 추가 정보가 포함되어 있습니다.

## <a name="make-sure-the-driver-you-want-is-installed"></a>원하는 드라이버가 설치되어 있는지 확인
1.  [제어판]에서 **ODBC 데이터 원본(64비트)** 애플릿을 검색하거나 찾아봅니다. 32비트 드라이버만 있거나 32비트 드라이버를 사용해야 한다는 것을 알고 있는 경우 **ODBC 데이터 원본(32비트)** 을 대신 검색하거나 찾아봅니다.
2.  애플릿을 시작합니다. **ODBC 데이터 원본 관리자** 창이 열립니다.
3.  **드라이버** 탭에서 컴퓨터에 설치된 모든 ODBC 드라이버의 목록을 찾을 수 있습니다. (일부 드라이버의 이름은 여러 언어로 나열될 수 있습니다.)

    다음은 설치된 64비트 드라이버 목록의 예입니다.

    ![설치된 64비트 ODBC 드라이버](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> 드라이버가 설치되어 있고 64비트 애플릿에 해당 드라이버가 표시되지 않는 경우 32비트 애플릿을 대신 찾습니다. 또한 64비트 또는 32비트 SQL Server 가져오기 및 내보내기 마법사를 실행해야 하는지 여부도 알려줍니다.
>
> 64비트 버전의 SQL Server 가져오기 및 내보내기 마법사를 사용하려면 SQL Server를 설치해야 합니다. SSDT(SQL Server Data Tools) 및 SSMS(SQL Server Management Studio)는 32비트 애플리케이션이며, 32비트 버전의 마법사를 포함하여 32비트 파일만 설치합니다.
    
## <a name="step-1---select-the-data-source"></a>1단계 - 데이터 원본 선택
컴퓨터에 설치된 ODBC 드라이버는 데이터 원본의 드롭다운 목록에 표시되지 않습니다. ODBC 드라이버로 연결하려면 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **.NET Framework Data Provider for ODBC**를 데이터 원본으로 선택하여 시작합니다. 이 공급자는 ODBC 드라이버 주위에서 래퍼 역할을 합니다.

다음은 .NET Framework Data Provider for ODBC를 선택한 직후 표시되는 일반적인 화면입니다.

![이전에 ODBC를 사용하여 SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>2단계 - 연결 정보 제공
다음 단계는 ODBC 드라이버 및 데이터 원본에 대한 연결 정보를 제공하는 것입니다. 두 가지 옵션이 있습니다.
1.  이미 존재하거나 [제어판]에서 **ODBC 데이터 원본 관리자** 애플릿으로 작성한 **DSN**(데이터 원본 이름)을 제공합니다. DSN은 ODBC 데이터 원본에 연결하는 데 필요한 설정의 저장된 컬렉션입니다.

    이미 DSN 이름을 알고 있거나 새 DSN을 만드는 방법을 알고 있으면 이 페이지의 나머지 부분은 건너뛸 수 있습니다. **데이터 원본 선택** 또는 **대상 선택** 페이지의 **Dsn** 필드에서 DSN 이름을 입력한 다음 마법사의 다음 단계를 계속 진행합니다.

    [DSN 제공](#odbc_dsn)
    
2.  **ODBC 데이터 원본 관리자** 애플릿을 사용하여 온라인 상태를 조회하거나 컴퓨터에서 만들고 테스트할 수 있는 **연결 문자열**을 제공합니다.

    이미 연결 문자열이 있거나 연결 문자열을 만드는 방법을 알고 있으면 이 페이지의 나머지 부분은 건너뛸 수 있습니다. **데이터 원본 선택** 또는 **대상 선택** 페이지의 **ConnectionString** 필드에서 연결 문자열을 입력한 다음 마법사의 다음 단계를 계속 진행합니다.

    [연결 문자열 제공](#odbc_connstring)

연결 문자열을 제공하면 마법사에서 데이터 원본에 연결하는 데 사용할 모든 연결 정보(예: 서버 및 데이터베이스 이름 및 인증 방법)가 **데이터 원본 선택** 또는 **대상 선택** 페이지에 표시됩니다. DSN을 제공하면 이 정보가 표시되지 않습니다.

## <a name="odbc_dsn"></a> 옵션 1 - DSN 제공
연결 정보에 DSN(데이터 원본 이름)을 제공하려면 **ODBC 데이터 원본 관리자** 애플릿을 사용하여 기존 DSN의 이름을 찾거나 새 DSN을 만듭니다.
1.  [제어판]에서 **ODBC 데이터 원본(64비트)** 애플릿을 검색하거나 찾아봅니다. 32비트 드라이버만 있거나 32비트 드라이버를 사용해야 하는 경우 **ODBC 데이터 원본(32비트)** 을 대신 검색하거나 찾아봅니다.
2.  애플릿을 시작합니다. **ODBC 데이터 원본 관리자** 창이 열립니다. 애플릿의 모양은 다음과 같습니다.

    ![ODBC 관리자 제어판 애플릿](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  데이터 원본으로 **기존 DSN을 사용**하려면 **사용자 DSN**, **시스템 DSN** 또는 **파일 DSN**  탭에 표시되는 DSN을 모두 사용할 수 있습니다. 이름을 확인한 다음 마법사로 돌아가서 **데이터 원본 선택** 또는 **대상 선택** 페이지의 **Dsn** 필드에서 해당 이름을 입력합니다. 이 페이지의 나머지 부분은 건너뛰고 마법사의 다음 단계를 계속 진행합니다.
4.  **새 DSN을 만들려면** 사용자(사용자 DSN)에게만 표시되거나, Windows 서비스가 포함된 컴퓨터의 모든 사용자(시스템 DSN)에게 표시되거나, 파일에 저장된 모든 사용자(파일 DSN)에게 표시되도록 할지 여부를 결정합니다. 이 예에서는 새 시스템 DSN을 만듭니다.
5. **시스템 DSN** 탭에서 **추가**를 클릭합니다.

    ![새 ODBC 시스템 DSN 추가](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  **새 데이터 원본 만들기** 대화 상자에서 데이터 원본에 대한 드라이버를 선택한 다음 **마침**을 클릭합니다.

    ![새 시스템 DSN에 대한 드라이버 선택](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. 이제 드라이버에서 데이터 원본에 연결하는 데 필요한 정보를 입력할 수 있는 하나 이상의 드라이버 관련 화면을 표시합니다. (예를 들어 SQL Server 드라이버의 경우 네 개의 사용자 지정 설정 페이지가 있습니다.) 완료되면 새 시스템 DSN이 목록에 표시됩니다.

    ![목록의 새 시스템 DSN](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  마법사로 돌아가서 **데이터 원본 선택** 또는 **대상 선택** 페이지의 **Dsn** 필드에서 DSN 이름을 입력합니다. 마법사의 다음 단계를 계속 진행합니다.

## <a name="odbc_connstring"></a> 옵션 2 - 연결 문자열 제공
연결 정보를 연결 문자열에 제공하려면 이 항목의 나머지 부분이 필요한 연결 문자열을 가져오는 데 도움이 됩니다.

이 예에서는 Microsoft SQL Server에 연결하는 다음 연결 문자열을 사용합니다.

    ```
    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
    ```

**데이터 원본 선택** 또는 **대상 선택** 페이지의 **ConnectionString** 필드에서 연결 문자열을 입력합니다. 연결 문자열을 입력하면 마법사에서 문자열을 구문 분석하고 개별 속성과 해당 값을 목록에 표시합니다.

다음은 연결 문자열을 입력한 후 표시되는 화면입니다.

![이후에 ODBC를 사용하여 SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> ODBC 드라이버에 대한 연결 옵션은 원본 또는 대상을 구성하는지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

## <a name="get-the-connection-string-online"></a>온라인으로 연결 문자열 가져오기
온라인으로 ODBC 드라이버에 대한 연결 문자열을 찾으려면 [연결 문자열 참조](https://www.connectionstrings.com/)를 참조하세요. 이 타사 사이트에는 샘플 연결 문자열과 필요한 데이터 공급자 및 연결 정보에 대한 추가 정보가 포함되어 있습니다.

## <a name="get-the-connection-string-with-an-app"></a>앱으로 연결 문자열 가져오기
사용자 컴퓨터에서 ODBC 드라이버에 대한 연결 문자열을 작성하고 테스트하려면 [제어판]에서 **ODBC 데이터 원본 관리자** 애플릿을 사용할 수 있습니다. 연결에 대한 파일 DSN을 만든 다음, 파일 DSN에서 설정을 복사하여 연결 문자열을 조합합니다. 이 작업에는 여러 단계가 필요하지만, 유효한 연결 문자열이 있는지 확인하는 데 도움이 됩니다.

1.  [제어판]에서 **ODBC 데이터 원본(64비트)** 애플릿을 검색하거나 찾아봅니다. 32비트 드라이버만 있거나 32비트 드라이버를 사용해야 하는 경우 **ODBC 데이터 원본(32비트)** 을 대신 검색하거나 찾아봅니다.
2.  애플릿을 시작합니다. **ODBC 데이터 원본 관리자** 창이 열립니다.
3.  이제 애플릿의 **파일 DSN** 탭으로 이동합니다. **추가**를 클릭합니다.

    이 예에서는 파일 DSN에서 연결 문자열에 필요한 특정 형식으로 이름-값 쌍을 저장하므로 사용자 DSN 또는 시스템 DSN 대신 파일 DSN을 만듭니다.

    ![새 ODBC 파일 DSN 추가](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  **새 데이터 원본 만들기** 대화 상자의 목록에서 드라이버를 선택하고 **다음**을 클릭합니다. 이 예에서는 Microsoft SQL Server에 연결하는 데 필요한 연결 문자열 인수가 포함된 DSN을 만듭니다.

    ![새 ODBC 데이터 원본 만들기](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  위치를 선택하고, 새 파일 DSN의 파일 이름을 입력하고, **다음**을 클릭합니다. 이후 단계에서 파일을 찾고 열 수 있도록 파일을 저장하는 위치를 기억합니다.

    ![새 파일 DSN 저장](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  선택 항목에 대한 요약을 검토하고 **마침**을 클릭합니다.

7.  **마침**을 클릭하면 선택한 드라이버에서 하나 이상의 전용 화면을 표시하여 연결하는 데 필요한 정보를 수집합니다. 일반적으로 이 정보에는 서버 기반 데이터 원본의 서버, 로그인 정보, 데이터베이스 및 파일 기반 데이터 원본의 파일, 형식, 버전이 포함됩니다.

8. 데이터 원본을 구성하고 **마침**을 클릭하면 일반적으로 선택 항목에 대한 요약이 표시되고 이를 테스트할 수 있습니다.

    ![새 파일 DSN 테스트](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. 데이터 원본을 테스트하고 대화 상자를 닫은 후에 파일 시스템에 저장한 파일 DSN을 찾습니다. 파일 확장명을 변경하지 않은 경우 기본 확장명은 .DSN입니다.

10. [메모장] 또는 다른 텍스트 편집기를 사용하여 저장된 파일을 엽니다. 다음은 SQL Server 예제의 내용입니다.

    ```   
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=MicrosoftÂ® WindowsÂ® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. 필요한 값을 복사하여 이름-값 쌍이 세미콜론으로 구분된 연결 문자열에 붙여넣습니다.

    파일 DSN 샘플에서 필요한 값을 조합하면 다음 연결 문자열이 있습니다.
    
        ```
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
        ```

    일반적으로 작동하는 연결 문자열을 만드는 데 ODBC 데이터 원본 관리자에서 만든 DSN 설정이 모두 필요하지는 않습니다.  
    -   ODBC 드라이버는 항상 지정해야 합니다.
    -   SQL Server와 같은 서버 기반 데이터 원본의 경우 일반적으로 서버, 데이터베이스 및 로그인 정보가 필요합니다. 따라서 DSN 샘플에는 TrustServerCertificate, WSID 또는 APP가 필요하지 않습니다.
    -   파일 기반 데이터 원본의 경우 적어도 파일 이름과 위치가 필요합니다.
    
12. 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **ConnectionString** 필드에 이 연결 문자열을 붙여넣습니다. 마법사에서 문자열을 구문 분석하고 계속할 준비가 되었습니다!

    ![이후에 ODBC를 사용하여 SQL에 연결](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>관련 항목:
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



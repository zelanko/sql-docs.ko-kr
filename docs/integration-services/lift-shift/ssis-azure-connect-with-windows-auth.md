---
title: "Windows 인증을 사용 하는 온-프레미스 데이터 원본에 연결 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1e3d9736612211038991489a4bd858d1ff89d333
ms.openlocfilehash: 1b60d877c6c75a77dd16fa8cb1704e10baf36bdb
ms.contentlocale: ko-kr
ms.lasthandoff: 10/19/2017

---
# <a name="connect-to-on-premises-data-sources-with-windows-authentication"></a>Windows 인증을 사용 하는 온-프레미스 데이터 원본에 연결
이 문서에서는 온-프레미스 데이터 원본에 연결 하는 데 Windows 인증을 사용 하는 패키지를 실행 하는 Azure SQL 데이터베이스에서 SSIS 카탈로그를 구성 하는 방법을 설명 합니다.

이 문서의 단계를 수행 하는 때를 제공 하는 도메인 자격 증명 변경 하거나 자격 증명을 제거 해야 SQL 데이터베이스 인스턴스에 대 한 모든 패키지 실행에 적용 됩니다.

## <a name="prerequisite"></a>필수 구성 요소
Windows 인증에 대 한 도메인 자격 증명을 설정 하기 전에 도메인 가입 된 컴퓨터에서 온-프레미스 데이터 원본에 연결할 수 있는지 여부를 확인 `runas` 모드입니다.

### <a name="connecting-to-sql-server"></a>SQL Server에 연결
온-프레미스 SQL Server에 연결할 수 있는지를 확인 하려면 다음 작업을 수행 합니다.

1.  이 테스트를 실행 하려면 도메인 가입 된 컴퓨터를 찾습니다.

2.  도메인 가입 된 컴퓨터에서 사용 하려는 도메인 자격 증명을 가진 SQL Server Management Studio (SSMS)를 시작 하려면 다음 명령을 실행 합니다.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  SSMS에서 사용 하려는 온-프레미스 SQL Server에 연결할 수 있는지 여부를 확인 합니다.

### <a name="connecting-to-a-file-share"></a>파일 공유에 연결
온-프레미스 파일 공유에 연결할 수 있는지를 확인 하려면 다음 작업을 수행 합니다.

1.  이 테스트를 실행 하려면 도메인 가입 된 컴퓨터를 찾습니다.

2.  도메인 가입 된 컴퓨터에서 다음 명령을 실행 합니다. 이 명령은 도메인 자격 증명을 사용 하려는 한 다음 파일 공유에 대 한 테스트 연결 디렉터리 목록을 가져와 명령 prommpt를 엽니다.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  디렉터리 목록이 반환 되는지 여부를 확인에 대 한 온-프레미스 파일 공유를 사용 하려면.

## <a name="provide-domain-credentials"></a>도메인 자격 증명을 제공 합니다.
패키지를 Windows 인증을 사용 하 여 온-프레미스 데이터 원본에 연결할 수 있도록 도메인 자격 증명을 제공 하려면 다음과 같은 작업을 수행 합니다.

1.  SQL Server Management Studio (SSMS) 또는 다른 도구는 SQL 데이터베이스에 연결 호스팅하는 SSIS 카탈로그 데이터베이스 (SSISDB). 자세한 내용은 참조 하십시오. [Azure에서 SSISDB 카탈로그 데이터베이스에 연결](ssis-azure-connect-to-catalog-database.md)합니다.

2.  현재 데이터베이스로 SSISDB를와 쿼리 창을 엽니다.

3.  다음 저장된 프로시저를 실행 하 고 적절 한 도메인 자격 증명을 제공 합니다.

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```
4.  SSIS 패키지를 실행 합니다. 패키지는 Windows 인증을 사용 하는 온-프레미스 데이터 원본에 연결 하는 데 제공 된 자격 증명을 사용 합니다.

## <a name="view-domain-credentials"></a>도메인 자격 증명 보기
활성 도메인 자격 증명을 보려면 다음 작업을 수행 합니다.

1.  SQL Server Management Studio (SSMS) 또는 다른 도구는 SQL 데이터베이스에 연결 호스팅하는 SSIS 카탈로그 데이터베이스 (SSISDB).

2.  현재 데이터베이스로 SSISDB를와 쿼리 창을 엽니다.

3.  다음 저장된 프로시저를 실행 하 고 출력을 확인 합니다.

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

## <a name="clear-domain-credentials"></a>일반 도메인 자격 증명
선택을 취소 하 고이 문서에 설명 된 대로 사용자가 제공한 자격 증명을 제거 하려면 다음과 같은 작업을 수행 합니다.

1.  SQL Server Management Studio (SSMS) 또는 다른 도구는 SQL 데이터베이스에 연결 호스팅하는 SSIS 카탈로그 데이터베이스 (SSISDB).

2.  현재 데이터베이스로 SSISDB를와 쿼리 창을 엽니다.

3.  다음 저장된 프로시저를 실행 합니다.

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-file-shares"></a>파일 공유에 연결
온-프레미스와 Azure 가상 컴퓨터에 모두 Azure SSIS 통합 런타임에서와 동일한 가상 네트워크에 파일 공유에 연결 하는 데 Windows 인증을 사용할 수 있습니다.

을 Azure 가상 컴퓨터에서 파일 공유에 연결 하려면 다음 작업을 수행 합니다.

1.  SQL Server Management Studio (SSMS) 또는 다른 도구는 SQL 데이터베이스에 연결 호스팅하는 SSIS 카탈로그 데이터베이스 (SSISDB).

2.  현재 데이터베이스로 SSISDB를와 쿼리 창을 엽니다.

3.  다음 저장된 프로시저를 실행 합니다.

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="next-steps"></a>다음 단계
- 패키지를 배포 합니다. 자세한 내용은 참조 하십시오. [SQL Server Management Studio (SSMS)와 SSIS 프로젝트 배포](../ssis-quickstart-deploy-ssms.md)합니다.
- 패키지를 실행 합니다. 자세한 내용은 참조 하십시오. [SSIS 패키지를 SQL Server Management Studio (SSMS)를 실행](../ssis-quickstart-run-ssms.md)합니다.
- 패키지를 예약 합니다. 자세한 내용은 참조 하십시오. [일정 SSIS 패키지를 Azure에서 실행](ssis-azure-schedule-packages.md)


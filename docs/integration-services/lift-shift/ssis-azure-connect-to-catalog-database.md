---
title: "Azure에서 SSISDB 카탈로그 데이터베이스에 연결 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: ac121e600c3c616006d79892c50f796ca7cd6b3f
ms.contentlocale: ko-kr
ms.lasthandoff: 10/13/2017

---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>Azure에서 SSISDB 카탈로그 데이터베이스에 연결

Azure SQL 데이터베이스 서버에서 호스팅되는 SSISDB 카탈로그 데이터베이스에 연결 하는 데 필요한 연결 정보를 가져옵니다. 다음 항목을 연결 해야 합니다.
- 정규화 된 서버 이름
- 데이터베이스 이름
- 로그인 정보 

## <a name="prerequisites"></a>필수 구성 요소
시작 하기 전에 17.2 SQL Server Management Studio의 이후 버전 지정 했는지 확인 합니다. 최신 버전의 SSMS 다운로드 하려면 [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.

## <a name="get-the-connection-info-from-the-azure-portal"></a>Azure 포털에서 연결 정보 가져오기
1. [Azure 포털](https://portal.azure.com/)에 로그인합니다.
2. Azure 포털에서 선택 **SQL 데이터베이스** 선택 고 왼쪽 메뉴의 `SSISDB` 데이터베이스에 **SQL 데이터베이스** 페이지. 
3. 에 **개요** 에 대 한 페이지는 `SSISDB` 데이터베이스, 다음 그림에 나와 있는 것 처럼 정규화 된 서버 이름을 검토 합니다. (를) 실행 서버 이름을 가리키면는 **에 복사 하려면 클릭** 옵션입니다.

    ![서버 연결 정보](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. SQL 데이터베이스 서버에 대 한 로그인 정보를 잊은 경우 SQL 데이터베이스 서버 페이지로 이동 합니다. 서버 관리자를 볼 수 있는 이름을 지정 하 고, 필요한 경우 암호를 다시 설정 합니다.

## <a name="connect-with-ssms"></a>SSMS를 사용 하 여 연결
1. SQL Server Management Studio를 엽니다.

2. **서버에 연결**합니다. 에 **서버에 연결** 대화 상자에서 다음 정보를 입력 합니다.

   | 설정       | 제안 된 값 | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수 사항입니다. |
   | **서버 이름** | 정규화 된 서버 이름 | 이 형식 이름 이어야 합니다: **mysqldbserver.database.windows.net**합니다. |
   | **인증** | SQL Server 인증(SQL Server Authentication) | 이 퀵 스타트의 SQL 인증을 사용 합니다. |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 이 서버를 만들 때 지정한 암호입니다. |

3. **SSISDB 데이터베이스에 연결**합니다. 선택 **옵션** 확장 하 고 **서버에 연결** 대화 상자. 확장 된 **서버에 연결** 대화 상자는 **연결 속성** 탭 합니다. 에 **연결할 데이터베이스** 필드를 선택 하거나 입력 `SSISDB`합니다.

    > [!IMPORTANT]
    > 선택 하지 않으면 `SSISDB` 개체 탐색기에서 SSIS 카탈로그를 보이지 않을 수 있음에 연결할 때.

4. 그런 다음 선택 **연결**합니다.

5. 개체 탐색기에서 확장 **Integration Services 카탈로그** 펼친 다음 **SSISDB** SSIS 카탈로그 데이터베이스에서 개체를 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 배포 합니다. 자세한 내용은 참조 하십시오. [SQL Server Management Studio (SSMS)와 SSIS 프로젝트 배포](../ssis-quickstart-deploy-ssms.md)합니다.
- 패키지를 실행 합니다. 자세한 내용은 참조 하십시오. [SSIS 패키지를 SQL Server Management Studio (SSMS)를 실행](../ssis-quickstart-run-ssms.md)합니다.
- 패키지를 예약 합니다. 자세한 내용은 참조 하십시오. [일정 SSIS 패키지를 Azure에서 실행](ssis-azure-schedule-packages.md)


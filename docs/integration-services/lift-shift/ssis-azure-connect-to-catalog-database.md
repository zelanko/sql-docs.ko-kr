---
title: "Azure에서 SSISDB 카탈로그 데이터베이스에 연결 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10be16cbc85cccce51fafbcd733045c653b7be0a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>Azure에서 SSISDB 카탈로그 데이터베이스에 연결

Azure SQL Database 서버에서 호스트되는 SSISDB 카탈로그 데이터베이스에 연결하는 데 필요한 연결 정보를 가져옵니다. 연결하려면 다음 항목이 필요합니다.
- 정규화된 서버 이름
- 데이터베이스 이름
- 로그인 정보 

## <a name="prerequisites"></a>필수 구성 요소
시작하기 전에 SQL Server Management Studio 버전 17.2 이상이 설치되어 있는지 확인합니다. SSMS의 최신 버전을 다운로드하려면 [SSMS(SQL Server Management Studio) 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 참조하세요.

## <a name="get-the-connection-info-from-the-azure-portal"></a>Azure Portal에서 연결 정보 가져오기
1. [Azure 포털](https://portal.azure.com/)에 로그인합니다.
2. Azure Portal의 왼쪽 메뉴에서 **SQL 데이터베이스**를 선택한 다음 **SQL 데이터베이스** 페이지에서 `SSISDB` 데이터베이스를 클릭합니다. 
3. `SSISDB` 데이터베이스의 **개요** 페이지에서 다음 이미지와 같이 정규화된 서버 이름을 검토합니다. 마우스로 서버 이름 위를 가리켜서 **복사하려면 클릭** 옵션을 표시합니다.

    ![서버 연결 정보](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. SQL Database 서버의 로그인 정보를 잊은 경우 SQL Database 서버 페이지로 이동합니다. 거기에서 서버 관리자 이름을 볼 수 있고 필요한 경우 암호를 재설정할 수 있습니다.

## <a name="connect-with-ssms"></a>SSMS를 사용하여 연결
1. SQL Server Management Studio를 엽니다.

2. **서버에 연결합니다**. **서버에 연결** 대화 상자에 다음 정보를 입력합니다.

   | 설정       | 제안된 값 | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수 사항입니다. |
   | **서버 이름** | 정규화된 서버 이름 | **mysqldbserver.database.windows.net** 형식이어야 합니다. |
   | **인증** | SQL Server 인증(SQL Server Authentication) | 이 빠른 시작에서는 SQL 인증을 사용합니다. |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 서버를 만들 때 지정한 암호입니다. |

3. **SSISDB 데이터베이스에 연결합니다**. **옵션**을 선택하여 **서버에 연결** 대화 상자를 펼칩니다. 펼쳐진 **서버에 연결** 대화 상자에서 **연결 속성** 탭을 선택합니다. **데이터베이스에 연결** 필드에서 `SSISDB`를 선택하거나 입력합니다.

    > [!IMPORTANT]
    > 연결할 때 `SSISDB`를 선택하지 않으면 개체 탐색기에 SSIS 카탈로그가 표시되지 않을 수 있습니다.

4. 그런 다음 **연결**을 선택합니다.

5. 개체 탐색기에서 **Integration Services 카탈로그**, **SSISDB**를 차례로 펼쳐 SSIS 카탈로그 데이터베이스의 개체를 봅니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 배포합니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 프로젝트 배포](../ssis-quickstart-deploy-ssms.md)를 참조하세요.
- 패키지를 실행합니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 패키지 실행](../ssis-quickstart-run-ssms.md)을 참조하세요.
- 패키지를 예약합니다. 자세한 내용은 [Azure에서 SSIS 패키지 실행 예약](ssis-azure-schedule-packages.md)을 참조하세요.

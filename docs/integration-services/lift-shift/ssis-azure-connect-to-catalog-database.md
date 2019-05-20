---
title: Azure에서 SSIS 카탈로그(SSISDB)에 연결 | Microsoft Docs
description: Azure SQL Database 서버에서 호스트된 SSIS 카탈로그(SSISDB)에 연결하는 데 필요한 연결 정보를 찾습니다.
ms.date: 09/23/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 2fd30ccac5cfb88d2b9258268ecc6844b78ddb53
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65721290"
---
# <a name="connect-to-the-ssis-catalog-ssisdb-in-azure"></a>Azure에서 SSIS 카탈로그(SSISDB)에 연결

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Azure SQL Database 서버에서 호스트된 SSIS 카탈로그(SSISDB)에 연결하는 데 필요한 연결 정보를 찾습니다. 연결하려면 다음 항목이 필요합니다.
- 정규화된 서버 이름
- 데이터베이스 이름
- 로그인 정보 

> [!IMPORTANT]
> 이번에는 Azure Data Factory에서 Azure-SSIS Integration Runtime을 만드는 작업과 독립적으로 Azure SQL Database에서 SSISDB 카탈로그 데이터베이스를 만들 수 없습니다. Azure-SSIS IR은 Azure에서 SSIS 패키지를 실행하는 런타임 환경입니다. 프로세스의 연습은 [Azure에서 SSIS 패키지 배포 및 실행](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)을 참조합니다. 

## <a name="prerequisites"></a>사전 요구 사항
시작하기 전에 SSMS(SQL Server Management Studio) 버전 17.2 이상이 설치되어 있는지 확인합니다. SSISDB 카탈로그 데이터베이스가 SQL Database Managed Instance에서 호스트될 경우 SSMS 버전이 17.6 이상인지 확인합니다. SSMS의 최신 버전을 다운로드하려면 [SSMS(SQL Server Management Studio) 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 참조하세요.

## <a name="get-the-connection-info-from-the-azure-portal"></a>Azure Portal에서 연결 정보 가져오기
1. [Azure 포털](https://portal.azure.com/)에 로그인합니다.
2. Azure Portal의 왼쪽 메뉴에서 **SQL 데이터베이스**를 선택한 다음 **SQL 데이터베이스** 페이지에서 `SSISDB` 데이터베이스를 클릭합니다. 
3. `SSISDB` 데이터베이스의 **개요** 페이지에서 다음 이미지와 같이 정규화된 서버 이름을 검토합니다. 마우스로 서버 이름 위를 가리켜서 **복사하려면 클릭** 옵션을 표시합니다.

    ![서버 연결 정보](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. SQL Database 서버의 로그인 정보를 잊은 경우 SQL Database 서버 페이지로 이동합니다. 거기에서 서버 관리자 이름을 볼 수 있고 필요한 경우 암호를 재설정할 수 있습니다.

## <a name="connect-with-ssms"></a>SSMS를 사용하여 연결
1. SQL Server Management Studio를 엽니다.

2. **서버에 연결합니다**. **서버에 연결** 대화 상자에 다음 정보를 입력합니다.

   | 설정       | 제안된 값 | 설명 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수 사항입니다. |
   | **서버 이름** | 정규화된 서버 이름 | **mysqldbserver.database.windows.net** 형식이어야 합니다. |
   | **인증** | SQL Server 인증(SQL Server Authentication) | |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 서버를 만들 때 지정한 암호입니다. |

    ![SSMS를 사용하여 서버에 연결](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-1.png)

3. **SSISDB 데이터베이스에 연결합니다**. **옵션**을 선택하여 **서버에 연결** 대화 상자를 펼칩니다. 펼쳐진 **서버에 연결** 대화 상자에서 **연결 속성** 탭을 선택합니다. **데이터베이스에 연결** 필드에서 `SSISDB`를 선택하거나 입력합니다.

    > [!IMPORTANT]
    > 연결할 때 `SSISDB`를 선택하지 않으면 개체 탐색기에 SSIS 카탈로그가 표시되지 않을 수 있습니다.

    ![연결할 SSISDB 데이터베이스 선택](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-2.png)

4. 그런 다음 **연결**을 선택합니다.

5. 개체 탐색기에서 **Integration Services 카탈로그**, **SSISDB**를 차례로 펼쳐 SSIS 카탈로그 데이터베이스의 개체를 봅니다.

    ![SSMS의 개체 탐색기에서 SSISDB 데이터베이스 찾기](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-3.png)

## <a name="next-steps"></a>다음 단계
- 패키지를 배포합니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 프로젝트 배포](../ssis-quickstart-deploy-ssms.md)를 참조하세요.
- 패키지를 실행합니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 패키지 실행](../ssis-quickstart-run-ssms.md)을 참조하세요.
- 패키지를 예약합니다. 자세한 내용은 [Azure에서 SSIS 패키지 예약](ssis-azure-schedule-packages.md) 참조

---
title: Stretch에 데이터베이스 사용 마법사를 실행하여 시작 | Microsoft 문서
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: quickstart
f1_keywords:
- sql13.swb.stretchwizard.f1
- sql13.swb.stretchwizard.createdatabasecredentials.f1
- sql13.swb.stretchwizard.selectdatabasetables.f1
- sql13.swb.stretchwizard.validatesqlserver.f1
- sql13.swb.stretchwizard.selectazuredeployment.f1
- sql13.swb.stretchwizard.configureazuredeployment.f1
- sql13.swb.stretchwizard.Summary.f1
- sql13.swb.stretchwizard.Results.f1
- sql13.swb.stretchwizard.introduction.f1
helpviewer_keywords:
- Stretch Database, wizard
- Enable Database for Stretch Wizard
ms.assetid: 855dd9fc-f80c-4dbc-bf46-55a9736bfe15
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 98c9691f51036b29aa80aa34b1ca8396ab49def2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62715594"
---
# <a name="get-started-by-running-the-enable-database-for-stretch-wizard"></a>Stretch에 데이터베이스 사용 마법사를 실행하여 시작
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 Stretch Database에 대한 데이터베이스를 구성하려면 Stretch에 데이터베이스 사용 마법사를 실행합니다.  이 문서에서는 입력해야 하는 정보와 마법사에서 선택해야 하는 항목에 대해 설명합니다.  
  
 스트레치 데이터베이스에 대해 자세히 알아보려면 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하세요. 
 
 > [!NOTE] 
 > 나중에 Stretch Database를 사용하지 않도록 설정하려는 경우 테이블 또는 데이터베이스에서 Stretch Database를 사용하지 않도록 설정하면 원격 개체가 삭제되지 않습니다. 원격 테이블 또는 원격 데이터베이스를 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다. 원격 개체는 수동으로 삭제할 때까지 Azure 비용이 계속해서 발생합니다. 
  
## <a name="launch-the-wizard"></a>마법사 시작  
  
1.  SQL Server Management Studio의 개체 탐색기에서 스트레치를 사용하도록 설정하려는 데이터베이스를 선택합니다.  
  
2.  마우스 오른쪽 단추를 클릭하고 **태스크**를 선택한 다음 **스트레치**를 선택하고 **사용** 을 선택하여 마법사를 시작합니다.  
  
##  <a name="Intro"></a> 소개  
 마법사의 용도 및 필수 구성 요소를 검토합니다.  
 
 중요 필수 구성 요소는 다음과 같습니다.
 -   데이터베이스 설정을 변경하려면 관리자여야 합니다.
 -   Microsoft Azure 구독을 보유해야 합니다.
 -   SQL Server에서 원격 Azure 서버와 통신할 수 있어야 합니다.
  
 ![Stretch Database 마법사의 소개 페이지](../../sql-server/stretch-database/media/stretch-wizard-1.png "Stretch Database 마법사의 소개 페이지")  
  
##  <a name="Tables"></a> 테이블 선택  
 스트레치에 사용할 테이블을 선택합니다.  
 
많은 행이 있는 테이블이 정렬된 목록 위쪽에 나타납니다. 마법사는 테이블 목록을 표시하기 전에 이를 분석하여 현재 Stretch Database에서 지원되지 않는 데이터 형식을 확인합니다. 
  
 ![Stretch Database 마법사의 테이블 선택 페이지](../../sql-server/stretch-database/media/stretch-wizard-2.png "Stretch Database 마법사의 테이블 선택 페이지")  
  
|Column|설명|  
|------------|-----------------|  
|(제목 없음)|선택한 테이블을 스트레치에 사용하려면 이 열에서 확인란을 선택합니다.|  
|**이름**|데이터베이스에서 테이블 이름을 지정합니다.|  
|(제목 없음)|이 열의 기호는 경고를 나타내지만 선택한 테이블에서 스트레치를 사용할 수는 있습니다. 또한 예를 들어 지원되지 않는 데이터 형식을 사용하는 등 선택한 테이블에서 스트레치를 사용하지 못하게 하는 차단 문제를 나타낼 수도 있습니다. 기호 위로 마우스를 올려 놓으면 도구 설명에 추가 정보가 표시됩니다. 자세한 내용은 [스트레치 데이터베이스에 대한 제한 사항](../../sql-server/stretch-database/limitations-for-stretch-database.md)을 참조하세요.|  
|**확대됨**|테이블이 이미 스트레치에 대해 활성화되었는지 여부를 나타냅니다.|  
|**마이그레이션**|전체 테이블(**전체 테이블**)을 마이그레이션하거나 테이블의 기존 열에 필터를 지정할 수 있습니다. 다른 필터 함수를 사용하여 마이그레이션할 행을 선택하려면 마법사를 종료한 다음 ALTER TABLE 문을 실행하여 필터 함수를 지정합니다. 필터 함수에 대한 자세한 내용은 [필터 함수를 사용하여 마이그레이션할 행 선택](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조하세요. 함수를 적용하는 방법은 [테이블에서 Stretch Database 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 또는 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.|  
|**행**|테이블의 행 수를 지정합니다.|  
|**크기(KB)**|테이블의 크기(KB)를 지정합니다.|  
  
## <a name="optionally-provide-a-row-filter"></a>필요에 따라 행 필터를 제공합니다.  
 마이그레이션할 행을 선택할 필터 함수를 제공하려면 **테이블 선택** 페이지에서 다음 중 하나를 수행합니다.  
  
1.  **확장할 테이블을 선택하세요.** 목록에서 테이블에 대한 행에 **전체 테이블** 을 클릭합니다. **스트레치할 행 선택** 대화 상자가 열립니다.  
  
     ![날짜를 기준으로 필터 조건자 정의](../../sql-server/stretch-database/media/stretch-wizard-2a.png "날짜를 기준으로 필터 조건자 정의")  
  
2.  **스트레치할 행 선택** 대화 상자에서 **행 선택**을 선택합니다.  
  
3.  **이름 필드**에 필터 함수의 이름을 제공합니다.  
  
4.  **Where** 절의 경우 테이블에서 열을 선택하고, 연산자를 선택한 다음 값을 제공합니다.  
  
5.  **확인** 을 클릭하여 함수를 테스트합니다. 함수에서 테이블의 결과를 반환하면, 즉 조건을 만족하는 마이그레이션할 행이 있는 경우 테스트에서 **성공**을 보고합니다.  

> [!NOTE] 
> 필터 쿼리를 표시하는 입력란은 읽기 전용입니다. 입력란의 쿼리를 편집할 수 없습니다.
  
6.  완료를 클릭하여 **테이블 선택** 페이지로 돌아갑니다.  

필터 함수는 마법사를 완료한 경우에만 SQL Server에서 생성됩니다. 그때까지는 **테이블 선택** 페이지로 돌아가 필터 함수를 변경하거나 이름을 바꿀 수 있습니다.

![필터 조건자를 정의한 후 테이블 선택 페이지](../../sql-server/stretch-database/media/stretch-wizard-2b.png "필터 조건자를 정의한 후 테이블 선택 페이지")

다른 유형의 필터 함수를 사용하여 마이그레이션할 행을 선택하려면 다음 중 하나를 수행합니다.  
  
-   마법사를 종료하고 ALTER TABLE 문을 실행하여 테이블에 대해 스트레치를 사용하도록 설정하고 필터 함수를 지정합니다. 자세한 내용은 [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)를 참조하세요.  
  
-   마법사를 종료한 후 ALTER TABLE 문을 실행하여 필터 함수를 지정합니다. 필수 단계는 [마법사를 실행한 후 필터 함수 추가](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz)를 참조하세요.  
  
##  <a name="Configure"></a> Azure 구성  
  
1.  Microsoft 계정을 사용하여 Microsoft Azure에 로그인합니다.  
  
     ![Azure에 로그인 - Stretch Database 마법사](../../sql-server/stretch-database/media/stretch-wizard-3.png "Azure에 로그인 - Stretch Database 마법사")  
  
2.  Stretch Database에 사용할 기존 Azure 구독을 선택합니다. 

> [!NOTE] 
> 데이터베이스에서 Stretch를 사용하도록 설정하려면 사용 중인 구독에 관리자 권한이 있어야 합니다. Stretch Database 마법사는 사용자가 관리자 권한이 있는 구독만 표시합니다.
  
3.  Stretch Database에 사용할 Azure 지역을 선택합니다.
    -   새 서버를 만들면 서버가 이 지역에 생성됩니다.  
    -   선택한 지역에 기존 서버가 있는 경우 **기존 서버**를 선택할 때 이러한 서버가 나열됩니다.
  
     대기 시간을 최소화하려면 SQL Server가 위치해 있는 Azure 지역을 선택합니다. 지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.  
  
4.  기존 서버를 사용할지, 새 Azure 서버를 만들지 지정합니다.  
  
     SQL Server의 Active Directory를 Azure Active Directory와 페더레이션하는 경우 필요에 따라 SQL Server가 원격 Azure 서버와 통신하는 데 페더레이션된 서비스 계정을 사용할 수 있습니다. 이 옵션의 요구 사항에 대한 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
    -   **새 서버 만들기**  
  
        1.  서버 관리자의 로그인과 암호를 만듭니다.  
  
        2.  필요에 따라 SQL Server가 원격 Azure 서버와 통신하는 데 페더레이션된 서비스 계정을 사용합니다.  
  
         ![새 Azure 서버 만들기 - Stretch Database 마법사](../../relational-databases/tables/media/stretch-wizard-4.png "새 Azure 서버 만들기 - Stretch Database 마법사")  
  
    -   **기존 서버**  
  
        1.  기존 Azure 서버를 선택합니다.  
  
        2.  인증 방법을 선택합니다.  
  
            -   **SQL Server 인증**을 선택하는 경우 관리 로그인 및 암호를 입력합니다.  
  
            -   SQL Server가 원격 Azure 서버와 통신하는 데 페더레이션된 서비스 계정을 사용하려면 **Active Directory 통합 인증** 을 선택합니다. 선택한 서버가 Azure Active Directory와 통합되어 있지 않으면 이 옵션이 표시되지 않습니다.
  
         ![기존 Azure 서버 선택 - Stretch Database 마법사](../../sql-server/stretch-database/media/stretch-wizard-5.png "기존 Azure 서버 선택 - Stretch Database 마법사")  
  
##  <a name="Credentials"></a> 보안 자격 증명  
 스트레치 데이터베이스가 원격 데이터베이스에 연결하기 위해 사용하는 자격 증명을 보호하기 위해 데이터베이스 마스터 키가 있어야 합니다.  
  
 데이터베이스 마스터 키가 이미 있는 경우 암호를 입력합니다.  
  
 ![Stretch Database 마법사의 보안 자격 증명 페이지](../../sql-server/stretch-database/media/stretch-wizard-6b.PNG "Stretch Database 마법사의 보안 자격 증명 페이지")  
  
 데이터베이스에 기존 마스터 키가 없는 경우 강력한 암호를 입력하여 데이터베이스 마스터 키를 만듭니다.  
  
 ![Stretch Database 마법사의 보안 자격 증명 페이지](../../relational-databases/tables/media/stretch-wizard-6.png "Stretch Database 마법사의 보안 자격 증명 페이지")  
  
 데이터베이스 마스터 키에 대한 자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) 및 [데이터베이스 마스터 키 만들기](../../relational-databases/security/encryption/create-a-database-master-key.md)를 참조하세요. 마법사에서 생성하는 자격 증명에 대한 자세한 내용은 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.  
  
##  <a name="Network"></a> IP 주소 선택  
 서브넷 IP 주소 범위(권장)를 사용하거나, SQL Server가 원격 Azure 서버와 통신할 수 있도록 Azure에서 방화벽 규칙을 만들기 위해 SQL Server의 공용 IP 주소를 사용합니다.  
  
 이 페이지에 제공된 IP 주소 또는 주소 범위를 통해 Azure 서버는 들어오는 데이터, 쿼리, SQL Server에서 시작한 관리 작업이 Azure Firewall을 통과하도록 허용합니다. 마법사는 SQL Server의 방화벽 설정에서 아무 것도 변경하지 않습니다.  
  
 ![Stretch Database 마법사의 IP 주소 선택 페이지](../../relational-databases/tables/media/stretch-wizard-7.png "Stretch Database 마법사의 IP 주소 선택 페이지")  
  
##  <a name="Summary"></a> 요약  
 마법사에서 입력한 값과 선택한 옵션, Azure에서 예상 비용을 검토합니다. 그런 다음 **마침** 을 선택하여 스트레치를 사용하도록 설정합니다.  
  
 ![Stretch Database 마법사의 요약 페이지](../../sql-server/stretch-database/media/stretch-wizard-8.png "Stretch Database 마법사의 요약 페이지")  
  
##  <a name="Results"></a> 결과  
 결과를 검토합니다.  
  
 데이터 마이그레이션 상태를 모니터링하려면 [데이터 마이그레이션 모니터링 및 문제 해결&#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)을 참조하세요.  
  
 ![Stretch Database 마법사의 결과 페이지](../../sql-server/stretch-database/media/stretch-wizard-9.PNG "Stretch Database 마법사의 결과 페이지")  
  
##  <a name="KnownIssues"></a> 마법사 문제 해결  
 **스트레치 데이터베이스 마법사가 실패했습니다.**  
 서버 수준에서 스트레치 데이터베이스가 아직 사용하도록 설정되지 않은 경우 시스템 관리자 권한 없이 마법사를 실행하여 사용하도록 설정하면 마법사가 실패합니다. 시스템 관리자에게 로컬 서버 인스턴스에서 스트레치 데이터베이스를 설정하도록 요청한 후 마법사를 다시 실행합니다. 자세한 내용은 [필수 구성 요소: 서버에서 Stretch Database를 활성화할 수 있는 권한](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md#EnableTSQLServer)을 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
 Stretch Database에 추가 테이블을 사용합니다. 데이터 마이그레이션을 모니터링하고 스트레치 사용 데이터베이스 및 테이블을 관리합니다.  
  
-   [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) : 추가 테이블을 사용합니다.  
  
-   데이터 마이그레이션 상태를 보려면 [데이터 마이그레이션 모니터링 및 문제 해결&#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)을 참조하세요.  
  
-   [데이터 마이그레이션 일시 중지 및 다시 시작&#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [스트레치 데이터베이스 관리 및 문제 해결](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [스트레치 사용 데이터베이스 백업](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [스트레치 사용 데이터베이스 복원](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  

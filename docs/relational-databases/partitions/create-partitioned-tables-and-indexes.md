---
title: 분할된 테이블 및 인덱스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.createpartition.progress.f1
- sql13.swb.createpartition.partitioncolumn.f1
- sql13.swb.createpartition.createjob.f1
- sql13.swb.createpartition.finish.f1
- sql13.swb.createpartition.selectoutput.f1
- sql13.swb.createpartition.partitionfunction.f1
- sql13.swb.createpartition.partitionscheme.f1
- sql13.swb.createpartition.getstart.f1
- sql13.swb.createpartition.mappartition.f1
- sql13.swb.createpartition.summary.f1
helpviewer_keywords:
- partitioned indexes [SQL Server], creating
- partition schemes [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], creating
- partition functions [SQL Server]
- partition schemes [SQL Server]
ms.assetid: 7641df10-1921-42a7-ba6e-4cb03b3ba9c8
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 147a5490d2940caebc9184e8049e7c430959b081
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787547"
---
# <a name="create-partitioned-tables-and-indexes"></a>분할된 테이블 및 인덱스 만들기
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 분할된 테이블 또는 인덱스를 만들 수 있습니다. 분할된 테이블 및 인덱스에 있는 데이터는 데이터베이스의 여러 파일 그룹에 분산할 수 있는 가로로 구분된 단위로 되어 있습니다. 큰 테이블과 인덱스를 분할하면 더 효율적으로 관리 및 확장할 수 있습니다.  
  
 분할된 테이블 또는 인덱스를 만드는 과정은 대개 다음 네 단계로 진행됩니다.  
  
1.  파티션 구성표에서 지정한 파티션을 보유할 파일 그룹 및 해당 파일을 만듭니다.  
  
2.  지정된 열 값을 기반으로 테이블 또는 인덱스의 행을 파티션에 매핑하는 파티션 함수를 만듭니다.  
  
3.  분할된 테이블 또는 인덱스의 파티션을 새 파일 그룹에 매핑하는 파티션 구성표를 만듭니다.  
  
4.  테이블 또는 인덱스를 만들거나 수정하고 파티션 구성표를 스토리지 위치로 지정합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **분할된 테이블 또는 인덱스를 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   파티션 함수 및 구성표의 범위는 해당 함수 및 구성표가 만들어진 데이터베이스로 제한됩니다. 데이터베이스 내에서 파티션 함수는 다른 함수와 서로 다른 네임스페이스에 있습니다.  
  
-   파티션 함수 내부의 행에 값이 null인 분할 열이 있으면 이러한 행은 가장 왼쪽의 파티션에 할당됩니다. 하지만 NULL이 경계 값으로 지정되고 RIGHT가 지정된 경우에는 맨 왼쪽 파티션이 빈 상태로 유지되고 NULL 값이 두 번째 파티션에 배치됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 분할된 테이블을 만들려면 데이터베이스에는 CREATE TABLE 권한이 필요하고 테이블을 만들 구성표에 대해서는 ALTER 권한이 필요합니다. 분할된 인덱스를 만들려면 인덱스를 만들 테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 분할된 테이블 또는 인덱스를 만들려면 다음과 같은 추가 권한 중 하나가 필요합니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 함수 및 파티션 구성표를 만들 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 함수 및 파티션 구성표를 만들 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 이 절차의 단계를 수행하여 하나 이상의 파일 그룹, 해당 파일 및 테이블을 만들 수 있습니다. 다음 절차에서 분할된 테이블을 만들 때 이 개체를 참조하게 됩니다.  
  
#### <a name="to-create-new-filegroups-for-a-partitioned-table"></a>분할된 테이블에 대한 새 파일 그룹을 만들려면  
  
1.  개체 탐색기에서 분할된 테이블을 만들 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **데이터베이스 속성 –** *database_name* 대화 상자의 **페이지 선택**에서 **파일 그룹**을 선택합니다.  
  
3.  **행**아래에서 **추가**를 클릭합니다. 새 행에 파일 그룹 이름을 입력합니다.  
  
    > [!WARNING]  
    >  파티션을 만들 경우 경계 값에 대해 지정된 수의 파일 그룹보다 파일 그룹이 한 개 더 있어야 합니다.  
  
4.  분할된 테이블에 대한 파일 그룹을 모두 만들 때까지 계속하여 행을 추가합니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  **페이지 선택**아래에서 **파일**을 선택합니다.  
  
7.  **행**아래에서 **추가**를 클릭합니다. 새 행에 파일 이름을 입력하고 파일 그룹을 선택합니다.  
  
8.  각 파일 그룹에 대해 하나 이상의 파일을 만들 때까지 계속하여 행을 추가 합니다.  
  
9. **테이블** 폴더를 확장하고 일반적인 방식으로 테이블을 만듭니다. 자세한 내용은 [테이블 만들기&#40;데이터베이스 엔진&#41;](../../relational-databases/tables/create-tables-database-engine.md)를 참조하세요. 또는 다음 절차에서 기존 테이블을 지정할 수도 있습니다.  
  
#### <a name="to-create-a-partitioned-table"></a>분할된 테이블을 만들려면  
  
1.  분할하려는 테이블을 마우스 오른쪽 단추로 클릭하고 **스토리지**를 가리킨 다음, **파티션 만들기...** 를 클릭합니다.  
  
2.  **파티션 작성 마법사**의 **파티션 작성 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **분할 열 선택** 페이지의 **사용 가능한 분할 열** 표에서 테이블을 분할할 열을 선택합니다. 데이터를 분할하는 데 사용할 수 있는 데이터 형식을 가진 열만 **사용 가능한 분할 열** 표에 표시됩니다. 계산 열을 분할 열로 선택하면 해당 열은 지속형 열로 지정되어야 합니다.  
  
     분할 열과 값 범위를 선택할 때는 논리적 방법으로 데이터를 그룹화할 수 있는 정도를 고려해야 합니다. 예를 들어 월 또는 연도의 분기에 따라 논리적 그룹으로 데이터를 분할하도록 선택할 수 있습니다. 데이터에 대해 만들게 될 쿼리에 따라 이 논리적 그룹이 테이블 파티션을 관리하기에 충분한지 여부가 결정됩니다. **text**, **ntext**, **image**, **xml**, **timestamp**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , 별칭 데이터 형식 또는 CLR 사용자 정의 데이터 형식을 제외한 모든 데이터 형식은 분할 열로 사용할 수 있습니다.  
  
     이 페이지에서는 다음과 같은 옵션을 추가로 선택할 수 있습니다.  
  
     **선택한 분할된 테이블에 맞춰 이 테이블 배치**  
     이 옵션을 선택하면 분할 열에서 이 테이블과 조인할 관련 데이터가 포함된 분할된 테이블을 선택할 수 있습니다. 분할 열에서 조인된 파티션이 있는 테이블의 쿼리는 일반적으로 더 효율적입니다.  
  
     **인덱싱된 파티션 열이 있는 고유하지 않은 인덱스 및 고유한 인덱스를 스토리지에 정렬**  
     동일한 파티션 구성표를 사용하여 분할된 테이블의 모든 인덱스를 정렬합니다. 테이블과 해당 인덱스가 정렬되면 데이터가 동일한 알고리즘으로 분할되므로 분할된 테이블의 안팎으로 보다 효율적으로 파티션을 이동할 수 있습니다.  
  
     분할 열 및 기타 옵션을 선택한 후 **다음**을 클릭합니다.  
  
4.  **파티션 함수 선택** 페이지의 **파티션 함수 선택**에서 **새 파티션 함수** 또는 **기존 파티션 함수**를 클릭합니다. **새 파티션 함수**를 선택하는 경우 함수 이름을 입력합니다. **기존 파티션 함수**를 선택하는 경우 사용하려는 함수 이름을 목록에서 선택합니다. 데이터베이스에 다른 파티션 함수가 없는 경우에는 **기존 파티션 함수** 옵션을 사용할 수 없습니다.  
  
     이 페이지를 마쳤으면 **다음**을 클릭합니다.  
  
5.  **파티션 구성표 선택** 페이지의 **파티션 구성표 선택**에서 **새 파티션 구성표** 또는 **기존 파티션 구성표**를 클릭합니다. **새 파티션 구성표**를 선택하는 경우 구성표 이름을 입력합니다. **기존 파티션 구성표**를 선택하는 경우 사용하려는 구성표 이름을 목록에서 선택합니다. 데이터베이스에 다른 파티션 구성표가 없는 경우에는 **기존 파티션 구성표** 옵션을 사용할 수 없습니다.  
  
     이 페이지를 마쳤으면 **다음**을 클릭합니다.  
  
6.  **파티션 매핑** 페이지의 **범위**에서 **왼쪽 경계** 또는 **오른쪽 경계** 중 하나를 선택하여 만들려는 각 파일 그룹 내에 최고 또는 최저 경계 값을 포함할지 여부를 지정합니다. 파티션을 만들 때 경계 값에 대해 지정된 파일 그룹의 수에 하나의 파일 그룹을 추가로 더해 입력해야 합니다.  
  
     **파일 그룹 선택 및 경계 값 지정** 표의 **파일 그룹**에서 데이터를 분할하여 저장할 파일 그룹을 선택합니다. **경계**아래에서 각 파일 그룹에 대한 경계 값을 입력합니다. 경계 값을 비워 두면 파티션 함수는 파티션 함수 이름을 사용하여 전체 테이블 또는 인덱스를 단일 파티션으로 매핑합니다.  
  
     이 페이지에서는 다음과 같은 옵션을 추가로 선택할 수 있습니다.  
  
     **경계 설정...**  
     **경계 값 설정** 대화 상자를 열어 파티션에 사용할 경계 값과 날짜 범위를 선택할 수 있습니다. 이 옵션은 **date**, **datetime**, **smalldatetime**, **datetime2**또는 **datetimeoffset**데이터 형식 중 하나를 포함하는 분할 열을 선택한 경우에만 사용할 수 있습니다.  
  
     **스토리지 계산**  
     파티션에 대해 지정된 각 파일 그룹에 대해 행 개수, 필요한 공간 및 사용 가능한 스토리지 공간을 예상합니다. 이러한 값은 표에 읽기 전용 값으로 표시됩니다.  
  
     **경계 값 설정** 대화 상자에서 다음 옵션을 추가로 선택할 수 있습니다.  
  
     **시작 날짜**  
     파티션의 범위 값에 대해 시작 날짜를 선택합니다.  
  
     **종료 날짜**  
     파티션의 범위 값에 대해 종료 날짜를 선택합니다. **파티션 매핑** 페이지에서 **왼쪽 경계** 를 선택한 경우 이 날짜가 각 파일 그룹/파티션의 마지막 값이 됩니다. **파티션 매핑** 페이지에서 **오른쪽 경계** 를 선택한 경우 이 날짜가 마지막에서 두 번째 파일 그룹의 첫 번째 값이 됩니다.  
  
     **날짜 범위**  
     각 파티션에 사용할 날짜 세분성이나 범위 값 증분을 선택합니다.  
  
     이 페이지를 마쳤으면 **다음**을 클릭합니다.  
  
7.  **출력 옵션 선택** 페이지에서 분할된 테이블을 완료하는 방법을 지정합니다. 마법사의 이전 페이지를 기반으로 SQL 스크립트를 만들려면 **스크립트 만들기** 를 선택합니다. 마법사의 남은 페이지를 모두 완료한 후 새 분할된 테이블을 만들려면 **즉시 실행** 을 선택합니다. 향후 미리 결정된 시간에 새 분할된 테이블을 만들려면 **일정** 을 선택합니다.  
  
     **스크립트 만들기**를 선택하는 경우 **스크립트 옵션**에서 다음과 같은 옵션을 사용할 수 있습니다.  
  
     **파일로 스크립팅**  
     스크립트를 .sql 파일로 생성합니다. **파일 이름** 상자에 파일 이름 및 위치를 입력하거나 **찾아보기** 를 클릭하여 **스크립트 파일 위치** 대화 상자를 엽니다. **다른 이름으로 저장**에서 **유니코드 텍스트** 또는 **ANSI 텍스트**를 선택합니다.  
  
     **클립보드로 스크립팅**  
     스크립트를 클립보드에 저장합니다.  
  
     **새 쿼리 창으로 스크립팅**  
     새 쿼리 편집기 창에 스크립트를 생성합니다. 이 옵션이 기본 옵션입니다.  
  
     **일정**을 선택하는 경우 **일정 변경**을 클릭합니다.  
  
    1.  **새 작업 일정** 대화 상자의 **이름** 상자에 작업 일정 이름을 입력합니다.  
  
    2.  **일정 유형** 목록에서 다음과 같은 일정 유형을 선택합니다.  
  
        -   **SQL Server 에이전트가 시작될 때 자동으로 시작**  
  
        -   **CPU가 유휴 상태로 될 때마다 시작**  
  
        -   **되풀이**. 새 분할된 테이블을 정기적으로 새로운 정보로 업데이트하는 경우 이 옵션을 선택합니다.  
  
        -   **한 번**. 이 옵션이 기본 옵션입니다.  
  
    3.  일정을 사용하거나 사용하지 않으려면 **사용** 확인란을 선택하거나 선택을 취소합니다.  
  
    4.  **되풀이**를 선택하는 경우 다음을 수행합니다.  
  
        1.  **빈도**아래의 **되풀이** 목록에서 다음과 같이 발생 빈도를 지정합니다.  
  
            -   **일별**을 선택하는 경우 **매** 상자에 작업 일정을 반복하는 일 수를 입력합니다.  
  
            -   **주별**을 선택하는 경우 **매** 상자에 작업 일정을 반복하는 주 수를 입력합니다. 작업 일정을 실행할 요일을 선택합니다.  
  
            -   **월별**을 선택한 경우 **매(Day)** 또는 **매(The)** 를 선택합니다.  
  
                -   **매(Day)** 를 선택한 경우 작업 일정을 실행할 날짜와 작업 일정을 반복할 월 수를 모두 입력합니다. 예를 들어 작업 일정을 격월로 15일에 실행하려면 **매(Day)** 를 선택하고 첫 번째 상자에 "15", 두 번째 상자에 "2"를 입력합니다. 두 번째 상자에 허용되는 가장 큰 숫자는 "99"입니다.  
  
                -   **매(The)** 를 선택한 경우 작업 일정을 실행할 요일 및 작업 일정을 반복할 월 수를 입력합니다. 예를 들어 작업 일정을 격월로 마지막 평일에 실행하려면 **매(Day)** 를 선택하고 첫 번째 목록에서 **마지막**, 두 번째 목록에서 **평일**을 선택한 다음, 마지막 상자에 "2"를 입력합니다. 처음 두 목록에서 **첫 번째**, **두 번째**, **세 번째**또는 **네 번째**및 특정 평일(예: 일요일 또는 수요일)을 선택할 수도 있습니다. 마지막 상자에 허용되는 가장 큰 숫자는 "99"입니다.  
  
        2.  **일별 빈도**에서 작업 일정이 실행되는 날에 작업 일정을 반복하는 빈도를 지정합니다.  
  
            -   **한 번 수행**을 선택하는 경우 **한 번 수행** 상자에 작업 일정을 실행할 특정 시간을 입력합니다. 시간, 분, 초와 오전 또는 오후를 입력합니다.  
  
            -   **되풀이 수행**을 선택하는 경우 **빈도**에 선택한 날 동안 작업 일정을 실행할 빈도를 지정합니다. 예를 들어 작업 일정을 실행하는 날에 2시간마다 작업 일정을 반복하려면 **되풀이 수행**을 선택하고 첫 번째 상자에 "2"를 입력한 다음, 목록에서 **시간**을 선택합니다. 이 목록에서 **분** 과 **초**도 선택할 수 있습니다. 첫 번째 상자에 허용되는 가장 큰 숫자는 "100"입니다.  
  
                 **시작** 상자에 작업 일정 실행을 시작할 시간을 입력합니다. **종료** 상자에 작업 일정 반복을 중지할 시간을 입력합니다. 시간, 분, 초와 오전 또는 오후를 입력합니다.  
  
        3.  **기간**아래의 **시작 날짜**에 작업 일정 실행을 시작할 날짜를 입력합니다. **종료 날짜** 또는 **종료 날짜 없음** 을 선택하여 작업 일정 실행을 중지할 시기를 나타냅니다. **종료 날짜**를 선택하는 경우 작업 일정 실행을 중지할 날짜를 입력합니다.  
  
    5.  **한 번**을 선택하는 경우 **한 번 발생**아래 **날짜** 상자에 작업 일정을 실행할 날짜를 입력합니다. **시간** 상자에 작업 일정을 실행할 시간을 입력합니다. 시간, 분, 초와 오전 또는 오후를 입력합니다.  
  
    6.  **요약**아래 **설명**에서 모든 작업 일정 설정이 올바른지 확인합니다.  
  
    7.  **확인**을 클릭합니다.  
  
     이 페이지를 마쳤으면 **다음**을 클릭합니다.  
  
8.  **요약 검토** 페이지의 **선택 항목 검토**아래에서 사용 가능한 옵션을 모두 확장하여 모든 파티션 설정이 올바른지 확인합니다. 모두 맞으면 **마침**을 클릭합니다.  
  
9. **파티션 작성 마법사 진행률** 페이지에서 파티션 작성 마법사의 동작에 대한 상태 정보를 모니터링할 수 있습니다. 마법사에서 선택한 옵션에 따라 진행률 페이지에 하나 이상의 동작이 포함될 수 있습니다. 맨 위에 있는 상자에는 전반적인 마법사 상태와 수신된 상태, 오류 및 경고 메시지의 수가 표시됩니다.  
  
     다음은 **파티션 작성 마법사 진행률** 페이지에서 선택할 수 있는 옵션입니다.  
  
     **세부 정보**  
     동작, 상태 및 마법사가 수행한 동작의 결과로 반환된 모든 메시지를 제공합니다.  
  
     **동작**  
     각 동작의 이름과 유형을 지정합니다.  
  
     **상태**  
     마법사 동작 결과 전체적으로 **성공** 값을 반환했는지 또는 **실패**값을 반환했는지 여부를 나타냅니다.  
  
     **메시지**  
     프로세스에서 반환된 모든 오류 또는 경고 메시지를 제공합니다.  
  
     **Report**  
     파티션 작성 마법사의 결과가 포함된 보고서를 만듭니다. **보고서 보기**, **보고서를 파일로 저장**, **클립보드에 보고서 복사**및 **보고서를 전자 메일로 보내기**중에서 선택할 수 있습니다.  
  
     **보고서 보기**  
     파티션 작성 마법사의 진행률에 대한 텍스트 보고서가 포함된 **보고서 보기** 대화 상자를 엽니다.  
  
     **보고서를 파일로 저장**  
     **보고서를 다른 이름으로 저장** 대화 상자를 엽니다.  
  
     **클립보드에 보고서 복사**  
     마법사의 진행률 보고서 결과를 클립보드에 복사합니다.  
  
     **보고서를 전자 메일로 보내기**  
     마법사의 진행률 보고서 결과를 이메일 메시지에 복사합니다.  
  
     완료되면 **닫기**를 클릭합니다.  
  
 파티션 만들기 마법사는 파티션 함수 및 스키마를 만들고 파티션을 지정된 테이블에 적용합니다. 테이블 파티션을 확인하려면 개체 탐색기에서 테이블을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **스토리지** 페이지를 클릭합니다. 이 페이지에는 파티션 함수 및 스키마 이름과 파티션 수와 같은 정보가 표시됩니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-partitioned-table"></a>분할된 테이블을 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 새 파일 그룹, 파티션 함수 및 파티션 스키마를 만듭니다. 스토리지 위치로 지정된 파티션 스키마를 사용하여 새 테이블을 만듭니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Adds four new filegroups to the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test1fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test4fg;   
  
    -- Adds one file for each filegroup.  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test1dat1,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat1.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test1fg;  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test2dat2,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t2dat2.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test3dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t3dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test4dat4,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t4dat4.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test4fg;  
    GO  
    -- Creates a partition function called myRangePF1 that will partition a table into four partitions  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
        AS RANGE LEFT FOR VALUES (1, 100, 1000) ;  
    GO  
    -- Creates a partition scheme called myRangePS1 that applies myRangePF1 to the four filegroups created above  
    CREATE PARTITION SCHEME myRangePS1  
        AS PARTITION myRangePF1  
        TO (test1fg, test2fg, test3fg, test4fg) ;  
    GO  
    -- Creates a partitioned table called PartitionTable that uses myRangePS1 to partition col1  
    CREATE TABLE PartitionTable (col1 int PRIMARY KEY, col2 char(10))  
        ON myRangePS1 (col1) ;  
    GO  
    ```  
  
#### <a name="to-determine-if-a-table-is-partitioned"></a>테이블이 분할되었는지 여부를 확인하려면  
  
1.  다음 쿼리는 `PartitionTable` 테이블이 분할된 경우 하나 이상의 행을 반환합니다. 테이블이 분할되지 않은 경우 행이 반환되지 않습니다.  
  
    ```  
    SELECT *   
    FROM sys.tables AS t   
    JOIN sys.indexes AS i   
        ON t.[object_id] = i.[object_id]   
        AND i.[type] IN (0,1)   
    JOIN sys.partition_schemes ps   
        ON i.data_space_id = ps.data_space_id   
    WHERE t.name = 'PartitionTable';   
    GO  
    ```  
  
#### <a name="to-determine-the-boundary-values-for-a-partitioned-table"></a>분할된 테이블에 대한 경계 값을 확인하려면  
  
1.  다음 쿼리는 `PartitionTable` 테이블의 각 파티션에 대해 경계 값을 반환합니다.  
  
    ```  
    SELECT t.name AS TableName, i.name AS IndexName, p.partition_number, p.partition_id, i.data_space_id, f.function_id, f.type_desc, r.boundary_id, r.value AS BoundaryValue   
    FROM sys.tables AS t  
    JOIN sys.indexes AS i  
        ON t.object_id = i.object_id  
    JOIN sys.partitions AS p  
        ON i.object_id = p.object_id AND i.index_id = p.index_id   
    JOIN  sys.partition_schemes AS s   
        ON i.data_space_id = s.data_space_id  
    JOIN sys.partition_functions AS f   
        ON s.function_id = f.function_id  
    LEFT JOIN sys.partition_range_values AS r   
        ON f.function_id = r.function_id and r.boundary_id = p.partition_number  
    WHERE t.name = 'PartitionTable' AND i.type <= 1  
    ORDER BY p.partition_number;  
    ```  
  
#### <a name="to-determine-the-partition-column-for-a-partitioned-table"></a>분할된 테이블에 대한 파티션 열을 확인하려면  
  
1.  다음 쿼리는 테이블에 대한 분할 열의 이름을 반환합니다. `PartitionTable`입니다.  
  
    ```  
    SELECT   
        t.[object_id] AS ObjectID   
        , t.name AS TableName   
        , ic.column_id AS PartitioningColumnID   
        , c.name AS PartitioningColumnName   
    FROM sys.tables AS t   
    JOIN sys.indexes AS i   
        ON t.[object_id] = i.[object_id]   
        AND i.[type] <= 1 -- clustered index or a heap   
    JOIN sys.partition_schemes AS ps   
        ON ps.data_space_id = i.data_space_id   
    JOIN sys.index_columns AS ic   
        ON ic.[object_id] = i.[object_id]   
        AND ic.index_id = i.index_id   
        AND ic.partition_ordinal >= 1 -- because 0 = non-partitioning column   
    JOIN sys.columns AS c   
        ON t.[object_id] = c.[object_id]   
        AND ic.column_id = c.column_id   
    WHERE t.name = 'PartitionTable' ;   
    GO  
    ```  
  
 자세한 내용은 다음을 참조하세요.  
  
-   [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
-   [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)  
  
-   [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)  
  
-   [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  

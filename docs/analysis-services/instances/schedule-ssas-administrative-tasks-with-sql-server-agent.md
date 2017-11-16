---
title: "SQL Server 에이전트와 SSAS 관리 태스크 예약 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d1484b3-51d9-48a0-93d2-0c3e4ed22b87
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 857540f661aa8eaecd42d98a648c03c043d06e2a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="schedule-ssas-administrative-tasks-with-sql-server-agent"></a>SQL Server 에이전트를 사용하여 SSAS 관리 태스크 예약
  SQL Server 에이전트 서비스를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리 작업을 예약하여 필요한 순서 및 시간에 실행할 수 있습니다. 예약된 태스크를 사용하면 정기적으로 또는 예측 가능한 주기에 따라 프로세스가 자동으로 실행되도록 할 수 있습니다. 비즈니스 활동을 수행하지 않는 시간 동안 큐브 처리 등의 관리 태스크가 실행되도록 예약할 수 있습니다. 또한 SQL Server 에이전트 작업 내에 작업 단계를 만들어 태스크 실행 순서를 지정할 수 있습니다. 예를 들어 큐브를 처리한 다음 큐브 백업을 수행할 수 있습니다.  
  
 작업 단계를 사용하면 실행 흐름을 제어할 수 있습니다. 한 작업이 실패한 경우 남아 있는 태스크를 계속 실행하거나 실행을 중지하도록 SQL Server 에이전트를 구성할 수 있습니다. 또한 작업 실행의 성공 또는 실패에 대한 알림을 보내도록 SQL Server 에이전트를 구성할 수 있습니다.  
  
 이 항목은 SQL Server 에이전트를 사용하여 XMLA 스크립트를 실행하는 두 가지 방법을 보여 주는 연습입니다. 첫 번째 예에서는 1차원 처리를 예약하는 방법을 보여 줍니다. 예 2에서는 처리 태스크를 일정대로 실행되는 단일 스크립트에 결합하는 방법을 보여 줍니다. 이 연습을 완료하려면 다음 사전 요구 사항을 충족해야 합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 SQL Server 에이전트 서비스가 설치되어 있어야 합니다.  
  
 기본적으로 서비스 계정으로 작업이 실행됩니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], SQL Server 에이전트용 기본 계정은 NT Service\SQLAgent$\<인스턴스 이름 >. 백업 또는 처리 태스크를 수행하려면 이 계정이 Analysis Services 인스턴스의 시스템 관리자여야 합니다. 자세한 내용은 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)를 참조하세요.  
  
 또한 작업에 사용할 테스트 데이터베이스가 있어야 합니다. AdventureWorks 다차원 예제 데이터베이스나 Analysis Services 다차원 자습서에 있는 프로젝트를 배포하여 이 연습에서 사용할 수 있습니다. 자세한 내용은 [Analysis Services 다차원 모델링 자습서에 사용할 예제 데이터 및 프로젝트 설치](../../analysis-services/install-sample-data-and-projects.md)을(를) 참조하세요.  
  
## <a name="example-1-processing-a-dimension-in-a-scheduled-task"></a>예제 1: 예약된 태스크에서 차원 처리  
 이 예에서는 차원을 처리하는 작업을 만들고 예약하는 방법을 보여 줍니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 예약된 태스크는 SQL Server 에이전트 작업에 포함되는 XMLA 스크립트입니다. 이 작업은 원하는 시간 또는 빈도로 실행하도록 예약됩니다. SQL Server 에이전트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일부이므로 데이터베이스 엔진 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 관리 태스크를 만들고 예약할 수 있습니다.  
  
###  <a name="bkmk_CreateScript"></a> SQL Server 에이전트 작업에서 차원 처리를 위한 스크립트 만들기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 연결합니다. 데이터베이스 폴더를 열고 차원을 찾습니다. 차원을 마우스 오른쪽 단추로 클릭하고 **처리**를 선택합니다.  
  
2.  **차원 처리** 대화 상자에 있는 **개체 목록** 의 **처리 옵션**열에서 이 열에 대한 옵션이 **전체 처리**인지 확인합니다. 그렇지 않을 경우 **처리 옵션**에서 해당 옵션을 클릭하고 드롭다운 목록에서 **전체 처리** 를 선택합니다.  
  
3.  **스크립트**를 클릭합니다.  
  
     이 단계에서 차원을 처리하는 XMLA 스크립트가 포함된 **XML 쿼리** 창이 열립니다.  
  
4.  **차원 처리** 대화 상자에서 **취소** 를 클릭하여 대화 상자를 닫습니다.  
  
5.  **XMLA 쿼리** 창에서 XMLA 스크립트를 강조 표시하고 강조된 스크립트를 마우스 오른쪽 단추로 클릭한 후 **복사**를 선택합니다.  
  
     이 단계에서 XMLA 스크립트를 Windows 클립보드에 복사합니다. XMLA 스크립트를 클립보드에 남겨 두거나 메모장 또는 다른 텍스트 편집기에 붙여 넣을 수 있습니다. 다음은 XMLA 스크립트의 예입니다.  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Account</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
###  <a name="bkmk_ProcessJob"></a> 차원 처리 작업 만들기 및 예약  
  
1.  데이터베이스 엔진 인스턴스에 연결한 후 개체 탐색기를 엽니다.  
  
2.  **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업** 을 마우스 오른쪽 단추로 클릭하고 **새 작업**을 선택합니다.  
  
4.  **새 작업** 대화 상자에서 **이름**에 작업 이름을 입력합니다.  
  
5.  **페이지 선택**에서 **단계**를 선택하고 **새로 만들기**를 클릭합니다.  
  
6.  **새 작업 단계** 대화 상자에서 **단계 이름**에 단계 이름을 입력합니다.  
  
7.  **서버**에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 기본 인스턴스에 대해 **localhost**를 입력하고 명명된 인스턴스에 대해 **localhost\\**\<*instance name*>를 입력합니다.  
  
     원격 컴퓨터에서 작업을 실행하려는 경우 작업을 실행할 서버 이름과 인스턴스 이름을 사용합니다. 형식을 사용 하 여 \< *서버 이름*> 기본 인스턴스에 대 한 및 \< *서버 이름*>\\<*인스턴스 이름*> 명명 된 인스턴스에 대 한 합니다.  
  
8.  **유형**에서 **SQL Server Analysis Services 명령**을 선택합니다.  
  
9. **명령**에서 마우스 오른쪽 단추를 클릭하고 **붙여넣기**를 선택합니다. 이전 단계에서 생성한 XMLA 스크립트가 명령 창에 나타나야 합니다.  
  
10. **확인**을 클릭합니다.  
  
11. **페이지 선택**에서 **일정**을 클릭한 후 **새로 만들기**를 클릭합니다.  
  
12. **새 작업 일정** 대화 상자에서 **이름**에 일정 이름을 입력하고 **확인**을 클릭합니다.  
  
     이 단계에서 일요일 오전 12시 일정을 만듭니다. 다음 단계에서는 수동으로 작업을 실행하는 방법을 보여 줍니다. 모니터링할 때 작업을 실행하는 일정을 지정할 수도 있습니다.  
  
13. **새 작업** 대화 상자에서 **확인**을 클릭합니다.  
  
14. **개체 탐색기**에서 **작업**을 확장하고 만들어진 작업을 마우스 오른쪽 단추로 클릭한 후 **작업 시작 단계**를 선택합니다.  
  
     작업에 단계가 하나뿐이므로 작업이 즉시 실행됩니다. 작업에 둘 이상의 단계가 있으면 작업을 시작할 단계를 선택할 수 있습니다.  
  
15. 작업이 끝나면 **닫기**를 클릭합니다.  
  
## <a name="example-2-batch-processing-a-dimension-and-a-partition-in-a-scheduled-task"></a>예제 2: 예약된 태스크에서 차원 및 파티션 일괄 처리  
 이 예의 절차는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 차원을 일괄 처리하는 작업을 만들고 예약하는 동시에 집계를 위해 차원에 종속되는 큐브 파티션을 처리하는 방법을 보여 줍니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 일괄 처리에 대한 자세한 내용은 [일괄 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)를 참조하세요.  
  
###  <a name="bkmk_BatchProcess"></a> SQL Server 에이전트 작업에서 차원 및 파티션 일괄 처리를 위한 스크립트 만들기  
  
1.  같은 데이터베이스를 사용하여 **차원**을 확장하고 **고객** 차원을 마우스 오른쪽 단추로 클릭한 다음 **처리**를 선택합니다.  
  
2.  **차원 처리** 대화 상자에 있는 **개체 목록** 의 **처리 옵션**열에서 이 열에 대한 옵션이 **전체 처리**인지 확인합니다.  
  
3.  **스크립트**를 클릭합니다.  
  
     이 단계에서 차원을 처리하는 XMLA 스크립트가 포함된 **XML 쿼리** 창이 열립니다.  
  
4.  **차원 처리** 대화 상자에서 **취소** 를 클릭하여 대화 상자를 닫습니다.  
  
5.  **큐브**, **Adventure Works**, **측정값 그룹**, **인터넷 판매**, **파티션**을 차례로 확장하고 목록의 마지막 파티션을 마우스 오른쪽 단추로 클릭한 다음 **처리**를 선택합니다.  
  
6.  **파티션 처리** 대화 상자에 있는 **개체 목록** 의 **처리 옵션**열에서 이 열에 대한 옵션이 **전체 처리**인지 확인합니다.  
  
7.  **스크립트**를 클릭합니다.  
  
     이 단계에서 파티션을 처리하는 XMLA 스크립트가 포함된 두 번째 **XML 쿼리** 창이 열립니다.  
  
8.  **파티션 처리** 대화 상자에서 **취소** 를 클릭하여 편집기를 닫습니다.  
  
     이때 두 스크립트를 병합하고 차원이 먼저 처리되도록 해야 합니다.  
  
    > [!WARNING]  
    >  파티션이 먼저 처리되고 이후에 차원이 처리되면 파티션이 처리되지 않습니다. 파티션을 두 번째로 처리해야 처리됨 상태가 됩니다.  
  
9. 파티션을 처리하는 XMLA 스크립트가 포함된 **XMLA 쿼리** 창에서 `Batch` 및 `Parallel` 태그 안의 코드를 강조 표시하고 강조된 스크립트를 마우스 오른쪽 단추로 클릭한 다음 **복사**를 선택합니다.  
  
    ```  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID> Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
    ```  
  
10. 차원을 처리하는 XMLA 스크립트가 포함된 **XMLA 쿼리** 창을 엽니다. `</Process>` 태그 왼쪽의 스크립트 내부를 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.  
  
     다음 예에서는 수정된 XMLA 스크립트를 보여 줍니다.  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Customer</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
11. 수정된 XMLA 스크립트를 강조 표시하고 강조된 스크립트를 마우스 오른쪽 단추로 클릭한 다음 **복사**를 선택합니다.  
  
12. 이 단계에서 XMLA 스크립트를 Windows 클립보드에 복사합니다. XMLA 스크립트를 클립보드에 남겨 두거나 파일에 저장하거나 메모장 또는 다른 텍스트 편집기에 붙여 넣을 수 있습니다.  
  
###  <a name="bkmk_Scheduling"></a> 일괄 처리 작업 만들기 및 예약  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 후 개체 탐색기를 엽니다.  
  
2.  **SQL Server 에이전트**를 확장합니다. 서비스가 실행되지 않았으면 서비스를 시작합니다.  
  
3.  **작업** 을 마우스 오른쪽 단추로 클릭하고 **새 작업**을 선택합니다.  
  
4.  **새 작업** 대화 상자에서 **이름**에 작업 이름을 입력합니다.  
  
5.  **단계**에서 **새로 만들기**를 클릭합니다.  
  
6.  **새 작업 단계** 대화 상자에서 **단계 이름**에 단계 이름을 입력합니다.  
  
7.  **유형**에서 **SQL Server Analysis Services 명령**을 선택합니다.  
  
8.  **다음 계정으로 실행**에서 **SQL Server 에이전트 서비스 계정**을 선택합니다. 사전 요구 사항 섹션에서 설명한 대로 이 계정에는 Analysis Services에 대한 관리 권한이 있어야 합니다.  
  
9. **서버**에서 Analysis Services 인스턴스의 서버 이름을 지정합니다.  
  
10. **명령**에서 마우스 오른쪽 단추를 클릭하고 **붙여넣기**를 선택합니다.  
  
11. **확인**을 클릭합니다.  
  
12. **일정** 페이지에서 **새로 만들기**를 클릭합니다.  
  
13. **새 작업 일정** 대화 상자에서 **이름**에 일정 이름을 입력하고 **확인**을 클릭합니다.  
  
     이 단계에서 일요일 오전 12시 일정을 만듭니다. 다음 단계에서는 수동으로 작업을 실행하는 방법을 보여 줍니다. 모니터링할 때 작업을 실행할 일정을 선택할 수도 있습니다.  
  
14. **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
15. **개체 탐색기**에서 **작업**을 확장하고 만들어진 작업을 마우스 오른쪽 단추로 클릭한 후 **작업 시작 단계**를 선택합니다.  
  
     작업에 단계가 하나뿐이므로 작업이 즉시 실행됩니다. 작업에 둘 이상의 단계가 있으면 작업을 시작할 단계를 선택할 수 있습니다.  
  
16. 작업이 끝나면 **닫기**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [처리 옵션 및 설정 &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)   
  
  


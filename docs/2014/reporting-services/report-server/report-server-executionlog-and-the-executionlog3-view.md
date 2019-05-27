---
title: 보고서 서버 실행 로그 및 ExecutionLog3 뷰 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- logs [Reporting Services], execution
- execution logs [Reporting Services]
ms.assetid: a7ead67d-1404-4e67-97e7-4c7b0d942070
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 649795e5e142563b64014f2ccf970f0df5de134b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103467"
---
# <a name="report-server-execution-log-and-the-executionlog3-view"></a>보고서 서버 실행 로그 및 ExecutionLog3 뷰
  보고서 서버 실행 로그에는 단일 서버 또는 기본 모드를 사용하는 스케일 아웃 배포 또는 SharePoint 팜을 사용한 다중 서버에서 실행되는 보고서에 대한 정보가 들어 있습니다. 보고서 실행 로그를 사용하여 보고서 요청 빈도, 가장 많이 사용되는 출력 형식 및 각 처리 단계에 소요된 처리 시간(밀리초)을 확인할 수 있습니다. 로그에는 보고서의 데이터 세트 쿼리 실행에 걸린 시간 또는 데이터 처리에 걸린 시간에 대한 정보가 포함됩니다. 보고서 서버 관리자는 로그 정보를 검토하여 오랫동안 실행되는 태스크를 식별하고 보고서 작성자가 보고서에서 기능을 향상시킬 수 있는 부문(데이터 세트 또는 처리)에 대한 사항을 제안할 수 있습니다.  
  
 SharePoint 모드용으로 구성된 보고서 서버는 또한 SharePoint ULS 로그를 활용할 수 있습니다. 자세한 내용은 [SharePoint 추적 로그에 대한 Reporting Services 이벤트 설정&#40;ULS&#41;](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)을 참조하세요.  
  
##  <a name="bkmk_top"></a> 로그 정보 보기  
 보고서 서버 실행은 내부 데이터베이스 테이블에 보고서 실행에 대한 데이터를 기록합니다. 테이블의 정보는 SQL Server 뷰에서 확인할 수 있습니다.  
  
 보고서 실행 로그는 기본적으로 이름이 **ReportServer**로 지정되는 보고서 서버 데이터베이스에 저장됩니다. SQL 뷰는 실행 로그 정보를 제공합니다. 최신 릴리스에는 "2"번과 "3"번 뷰가 추가되었으며, 이러한 뷰에는 새로운 필드 또는 이전 릴리스보다 친숙한 이름의 필드가 포함됩니다. 이전 뷰도 제품에 그대로 유지되므로 이러한 뷰를 사용하는 사용자 지정 애플리케이션에는 영향을 주지 않습니다. 이전 뷰에 대한 종속성이 없는 경우(예: ExecutionLog) 최신 뷰인 ExecutionLog**3**를 사용하는 것이 좋습니다.  
  
 항목 내용  
  
-   [SharePoint 모드 보고서 서버에 대한 구성 설정](#bkmk_sharepoint)  
  
-   [기본 모드 보고서 서버에 대한 구성 설정](#bkmk_native)  
  
-   [로그 필드(ExecutionLog3)](#bkmk_executionlog3)  
  
-   [AdditionalInfo 필드](#bkmk_additionalinfo)  
  
-   [로그 필드(ExecutionLog2)](#bkmk_executionlog2)  
  
-   [로그 필드(ExecutionLog)](#bkmk_executionlog)  
  
##  <a name="bkmk_sharepoint"></a> SharePoint 모드 보고서 서버에 대한 구성 설정  
 보고서 실행 로깅은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션의 시스템 설정에서 설정 또는 해제할 수 있습니다.  
  
 기본적으로 로그 항목은 60일 동안 보관됩니다. 이 날짜를 초과한 항목은 매일 오전 2시에 제거됩니다. 제대로 된 설치에서는 항상 60일 동안의 정보만 사용할 수 있게 됩니다.  
  
 로깅된 행 수와 항목 유형에 대한 제한을 설정할 수 없습니다.  
  
 **실행 로깅을 설정하려면**  
  
1.  SharePoint 중앙 관리의 **애플리케이션 관리** 그룹에서 **서비스 애플리케이션 관리** 를 클릭합니다.  
  
2.  구성하려는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션의 이름을 클릭합니다.  
  
3.  **시스템 설정**을 클릭합니다.  
  
4.  **로깅** 섹션에서 **실행 로깅 사용** 을 선택합니다.  
  
5.  **확인**을 클릭합니다.  
  
 **자세한 로깅을 설정하려면**  
  
 이전 단계에 설명된 대로 로깅을 설정한 후 다음을 완료해야 합니다.  
  
1.  **서비스 응용 프로그램의** 시스템 설정 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지에서 **사용자 정의** 섹션을 찾습니다.  
  
2.  **ExecutionLogLevel** 을 **자세히**로 변경합니다. 이 필드는 텍스트 입력 필드이며 **자세히** 및 **보통**중에서 값을 선택할 수 있습니다.  
  
##  <a name="bkmk_native"></a> 기본 모드 보고서 서버에 대한 구성 설정  
 SQL Server Management Studio의 서버 속성 페이지에서 보고서 실행 로깅을 설정하거나 해제할 수 있습니다. **EnableExecutionLogging** 은 고급 속성입니다.  
  
 기본적으로 로그 항목은 60일 동안 보관됩니다. 이 날짜를 초과한 항목은 매일 오전 2시에 제거됩니다. 제대로 된 설치에서는 항상 60일 동안의 정보만 사용할 수 있게 됩니다.  
  
 로깅된 행 수와 항목 유형에 대한 제한을 설정할 수 없습니다.  
  
 **실행 로깅을 설정하려면**  
  
1.  관리 권한을 사용하여 SQL Server Management Studio를 시작합니다. 예를 들어 Management Studio 아이콘을 마우스 오른쪽 단추로 클릭하고 '관리자 권한으로 실행'을 클릭합니다.  
  
2.  원하는 보고서 서버에 연결합니다.  
  
3.  서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. 속성 옵션이 해제되어 있으면 관리 권한을 사용하여 SQL Server Management Studio를 실행했는지 확인합니다.  
  
4.  **로깅** 페이지를 클릭합니다.  
  
5.  **보고서 실행 로깅 사용**을 선택합니다.  
  
 **자세한 로깅을 설정하려면**  
  
 이전 단계에 설명된 대로 로깅을 설정한 후 다음을 완료해야 합니다.  
  
1.  **서버 속성** 대화 상자에서 **고급** 페이지를 클릭합니다.  
  
2.  **사용자 정의** 섹션에서 **ExecutionLogLevel** 을 **자세히**로 변경합니다. 이 필드는 텍스트 입력 필드이며 **자세히** 및 **보통**중에서 값을 선택할 수 있습니다.  
  
##  <a name="bkmk_executionlog3"></a> 로그 필드(ExecutionLog3)  
 이 뷰에는 XML 기반 **AdditionalInfo** 열 안에 추가 성능 진단 노드가 추가되었습니다. AdditionalInfo 열에는 여러 추가 정보 필드에 대한 1의 XML 구조가 포함되어 있습니다. 다음은 ExecutionLog3 뷰에서 행을 검색하는 샘플 Transact SQL 문입니다. 이 샘플에서는 보고서 서버 데이터베이스 이름이 **ReportServer**라고 가정합니다.  
  
```  
Use ReportServer  
select * from ExecutionLog3 order by TimeStart DESC  
```  
  
 다음 표에서는 보고서 실행 로그에 캡처되는 데이터에 대해 설명합니다.  
  
|Column|Description|  
|------------|-----------------|  
|InstanceName|요청을 처리한 보고서 서버 인스턴스 이름 사용자 환경에 보고서 서버가 두 개 이상 포함된 경우 InstanceName 배포를 분석하여 네트워크 부하 분산 장치가 예상한 대로 보고서 서버 간에 요청을 분배하는지 모니터링 및 확인할 수 있습니다.|  
|ItemPath|보고서 또는 보고서 항목이 저장된 위치의 경로|  
|UserName|사용자 식별자|  
|ExecutionID|요청과 연결된 내부 식별자입니다. 동일한 사용자 세션에 대한 요청은 같은 실행 ID를 공유합니다.|  
|RequestType|가능한 값은 다음과 같습니다.<br />**대화형**<br />**구독**<br /><br /> <br /><br /> RequestType=Subscription으로 필터링되고 TimeStart로 정렬된 로그 데이터를 분석하면 구독 사용량이 많은 기간을 확인할 수 있으며, 그에 따라 보고서 구독 중 일부를 다른 시간으로 수정해야 할 수 있습니다.|  
|형식|렌더링 형식|  
|매개 변수|보고서 실행에 사용된 매개 변수 값|  
|ItemAction|가능한 값은 다음과 같습니다.<br /><br /> **Render**<br /><br /> **Sort**<br /><br /> **BookMarkNavigation**<br /><br /> **DocumentNavigation**<br /><br /> **GetDocumentMap**<br /><br /> **Findstring**<br /><br /> **실행**<br /><br /> **RenderEdit**|  
|TimeStart|보고서 처리 기간을 나타내는 시작 및 중지 시간|  
|TimeEnd||  
|TimeDataRetrieval|데이터를 검색하는 데 걸린 시간(밀리초)|  
|TimeProcessing|보고서를 처리하는 데 걸린 시간(밀리초)|  
|TimeRendering|보고서를 렌더링하는 데 걸린 시간(밀리초)|  
|원본|보고서 실행의 원본입니다. 가능한 값은 다음과 같습니다.<br /><br /> **라이브**<br /><br /> **캐시**: 쿼리 라이브로 실행 되지 않은 데이터 집합에 예를 들어, 캐시 된 실행을 나타냅니다.<br /><br /> **스냅숏**<br /><br /> **기록**<br /><br /> **AdHoc** : 동적으로 생성 된 보고서 모델 기반 드릴스루 보고서 또는 처리 및 렌더링에 대 한 보고서 서버를 활용 하는 클라이언트에 미리 본 보고서 작성기 보고서를 나타냅니다.<br /><br /> **세션**: 요청이 이미 설정 된 세션 안의 후속을 나타냅니다.  예를 들어 초기 요청은 1페이지를 보는 것이고 후속 요청은 현재 세션 상태로 Excel로 내보내는 것입니다.<br /><br /> **Rdce**:  Report Definition Customization Extension을 나타냅니다. RDCE 사용자 지정 확장 프로그램에서는 보고서 실행 시 보고서 정의가 처리 엔진에 전달되기 전에 보고서 정의를 동적으로 사용자 지정할 수 있습니다.|  
|상태|상태(rsSuccess 또는 오류 코드: 여러 개의 오류가 발생하면 첫 번째 오류만 기록됨)|  
|ByteCount|렌더링된 보고서 크기(바이트)|  
|RowCount|쿼리에서 반환된 행 수|  
|AdditionalInfo|실행에 대한 추가 정보가 포함된 XML 속성 모음 콘텐츠는 각 행마다 서로 다를 수 있습니다.|  
  
##  <a name="bkmk_additionalinfo"></a> AdditionalInfo 필드  
 AdditionalInfo 필드는 실행에 대한 추가 정보가 포함된 XML 속성 모음 또는 구조입니다. 콘텐츠는 로그에서 각 행마다 서로 다를 수 있습니다.  
  
 다음 표는 표준 및 자세한 로깅에 대한 AddtionalInfo 필드 내용의 예입니다.  
  
 **Addtionalinfo의 표준 로깅 예**  
  
```  
<AdditionalInfo>  
  <ProcessingEngine>2</ProcessingEngine>  
  <ScalabilityTime>  
    <Pagination>0</Pagination>  
    <Processing>0</Processing>  
  </ScalabilityTime>  
  <EstimatedMemoryUsageKB>  
    <Pagination>0</Pagination>  
    <Processing>6</Processing>  
  </EstimatedMemoryUsageKB>  
  <DataExtension>  
    <SQL>1</SQL>  
  </DataExtension>  
  <Connections>  
    <Connection>  
      <ConnectionOpenTime>147</ConnectionOpenTime>  
      <DataSets>  
        <DataSet>  
          <Name>DataSet1</Name>  
          <RowsRead>16</RowsRead>  
          <TotalTimeDataRetrieval>642</TotalTimeDataRetrieval>  
          <ExecuteReaderTime>63</ExecuteReaderTime>  
        </DataSet>  
        <DataSet>  
          <Name>DataSet2</Name>  
          <RowsRead>3</RowsRead>  
          <TotalTimeDataRetrieval>157</TotalTimeDataRetrieval>  
          <ExecuteReaderTime>60</ExecuteReaderTime>  
        </DataSet>  
      </DataSets>  
    </Connection>  
  </Connections>  
</AdditionalInfo>  
  
```  
  
 **Addtionalinfo의 자세한 로깅 예**  
  
```  
<AdditionalInfo>  
  <ProcessingEngine>2</ProcessingEngine>  
  <ScalabilityTime>  
    <Pagination>0</Pagination>  
    <Processing>0</Processing>  
  </ScalabilityTime>  
  <EstimatedMemoryUsageKB>  
    <Pagination>0</Pagination>  
    <Processing>6</Processing>  
  </EstimatedMemoryUsageKB>  
  <DataExtension>  
    <SQL>1</SQL>  
  </DataExtension>  
  <Connections>  
    <Connection>  
      <ConnectionOpenTime>127</ConnectionOpenTime>  
      <DataSource>  
        <Name>DataSource1</Name>  
        <DataExtension>SQL</DataExtension>  
      </DataSource>  
      <DataSets>  
        <DataSet>  
          <Name>DataSet1</Name>  
          <RowsRead>16</RowsRead>  
          <TotalTimeDataRetrieval>655</TotalTimeDataRetrieval>  
          <QueryPrepareAndExecutionTime>94</QueryPrepareAndExecutionTime>  
          <ExecuteReaderTime>33</ExecuteReaderTime>  
          <DataReaderMappingTime>30</DataReaderMappingTime>  
          <DisposeDataReaderTime>1</DisposeDataReaderTime>  
        </DataSet>  
        <DataSet>  
          <Name>DataSet2</Name>  
          <RowsRead>3</RowsRead>  
          <TotalTimeDataRetrieval>16</TotalTimeDataRetrieval>  
          <QueryPrepareAndExecutionTime>2</QueryPrepareAndExecutionTime>  
          <ExecuteReaderTime>1</ExecuteReaderTime>  
          <DataReaderMappingTime>0</DataReaderMappingTime>  
          <DisposeDataReaderTime>0</DisposeDataReaderTime>  
        </DataSet>  
      </DataSets>  
    </Connection>  
  </Connections>  
</AdditionalInfo>  
  
```  
  
 다음 AdditionalInfo 필드에 표시 되는 속성 중 일부를 설명 합니다.  
  
-   **ProcessingEngine**: 1=SQL Server 2005, 2=새로운 요청 시 처리 엔진. 대부분의 보고서에 값이 계속 1로 표시되면 보다 효율적이고 새로운 요청 시 처리 엔진을 활용할 수 있도록 보고서를 다시 디자인할 방법을 조사해야 할 수 있습니다.  
  
     `<ProcessingEngine>2</ProcessingEngine>`  
  
-   **ScalabilityTime**: 처리 엔진에서 확장 관련 작업을 수행하는 데 걸린 시간(밀리초)입니다. 값이 0이면 확장 작업에 추가 시간이 걸리지 않았으며, 해당 요청이 메모리 부담을 주지 않은 것을 나타냅니다.  
  
    ```  
    <ScalabilityTime>  
        <Processing>0</Processing>  
    </ScalabilityTime>  
    ```  
  
-   **EstimatedMemoryUsageKB**: 특정 요청 중에 각 구성 요소에서 소비될 것으로 예상되는 최대 메모리 양(KB)  
  
    ```  
    <EstimatedMemoryUsageKB>  
        <Processing>38</Processing>  
    </EstimatedMemoryUsageKB>  
    ```  
  
-   **DataExtension**: 보고서에 사용된 데이터 확장 또는 데이터 원본의 유형입니다. 이 수치는 특정 데이터 원본의 발생 횟수입니다.  
  
    ```  
    <DataExtension>  
       <DAX>2</DAX>  
    </DataExtension>  
    ```  
  
-   **ExternalImages**값은 밀리초에서 단위입니다. 이 데이터를 사용하여 성능 문제를 진단할 수 있습니다. 외부 웹 서버에서 이미지를 검색하는 데 필요한 시간으로 인해 전반적인 보고서 실행 속도가 느려질 수 있습니다. 추가 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]합니다.  
  
    ```  
    <ExternalImages>  
        <Count>3</Count>  
        <ByteCount>9268</ByteCount>  
        <ResourceFetchTime>9</ResourceFetchTime>  
    </ExternalImages>  
    ```  
  
-   **연결**: 여러 수준의 구조입니다. 추가 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]합니다.  
  
    ```  
    <Connections>  
        <Connection>  
          <ConnectionOpenTime>127</ConnectionOpenTime>  
          <DataSource>  
            <Name>DataSource1</Name>  
            <DataExtension>SQL</DataExtension>  
          </DataSource>  
          <DataSets>  
            <DataSet>  
              <Name>DataSet1</Name>  
              <RowsRead>16</RowsRead>  
              <TotalTimeDataRetrieval>655</TotalTimeDataRetrieval>  
              <QueryPrepareAndExecutionTime>94</QueryPrepareAndExecutionTime>  
              <ExecuteReaderTime>33</ExecuteReaderTime>  
              <DataReaderMappingTime>30</DataReaderMappingTime>  
              <DisposeDataReaderTime>1</DisposeDataReaderTime>  
            </DataSet>  
            <DataSet>  
              <Name>DataSet2</Name>  
              <RowsRead>3</RowsRead>  
              <TotalTimeDataRetrieval>16</TotalTimeDataRetrieval>  
              <QueryPrepareAndExecutionTime>2</QueryPrepareAndExecutionTime>  
              <ExecuteReaderTime>1</ExecuteReaderTime>  
              <DataReaderMappingTime>0</DataReaderMappingTime>  
              <DisposeDataReaderTime>0</DisposeDataReaderTime>  
            </DataSet>  
          </DataSets>  
        </Connection>  
    </Connections>  
  
    ```  
  
##  <a name="bkmk_executionlog2"></a> 로그 필드(ExecutionLog2)  
 이 뷰에는 몇 가지 새로운 필드가 추가되었으며, 다른 일부 필드는 이름이 바뀌었습니다. 다음은 ExecutionLog2 뷰에서 행을 검색하는 샘플 Transact SQL 문입니다. 이 샘플에서는 보고서 서버 데이터베이스 이름이 **ReportServer**라고 가정합니다.  
  
```  
Use ReportServer  
select * from ExecutionLog2 order by TimeStart DESC  
```  
  
 다음 표에서는 보고서 실행 로그에 캡처되는 데이터에 대해 설명합니다.  
  
|Column|Description|  
|------------|-----------------|  
|InstanceName|요청을 처리한 보고서 서버 인스턴스 이름|  
|ReportPath|보고서의 경로 구조입니다.  예를 들어 보고서 관리자의 루트 폴더에 있고 이름이 "test"인 보고서의 ReportPath는 "/test"입니다.<br /><br /> 보고서 관리자에서 "samples" 폴더에 저장된 이름이 "test"인 보고서의 ReportPath는 "/Samples/test"입니다.|  
|UserName|사용자 식별자|  
|ExecutionID||  
|RequestType|요청 형식(사용자 또는 시스템)|  
|형식|렌더링 형식|  
|매개 변수|보고서 실행에 사용된 매개 변수 값|  
|ReportAction|가능한 값: Render, Sort, BookMarkNavigation, DocumentNavigation, GetDocumentMap, Findstring|  
|TimeStart|보고서 처리 기간을 나타내는 시작 및 중지 시간|  
|TimeEnd||  
|TimeDataRetrieval|데이터 검색, 보고서 처리 및 보고서 렌더링에 걸린 시간(밀리초 단위)|  
|TimeProcessing||  
|TimeRendering||  
|원본|보고서 실행 원본(1=라이브, 2=캐시, 3=스냅숏, 4=기록)|  
|상태|상태(rsSuccess 또는 오류 코드: 여러 개의 오류가 발생하면 첫 번째 오류만 기록됨)|  
|ByteCount|렌더링된 보고서 크기(바이트)|  
|RowCount|쿼리에서 반환된 행 수|  
|AdditionalInfo|실행에 대한 추가 정보가 포함된 XML 속성 모음|  
  
##  <a name="bkmk_executionlog"></a> 로그 필드(ExecutionLog)  
 다음은 ExecutionLog 뷰에서 행을 검색하는 샘플 Transact SQL 문입니다. 이 샘플에서는 보고서 서버 데이터베이스 이름이 **ReportServer**라고 가정합니다.  
  
```  
Use ReportServer  
select * from ExecutionLog order by TimeStart DESC  
  
```  
  
 다음 표에서는 보고서 실행 로그에 캡처되는 데이터에 대해 설명합니다.  
  
|Column|Description|  
|------------|-----------------|  
|InstanceName|요청을 처리한 보고서 서버 인스턴스 이름|  
|ReportID|보고서 식별자|  
|UserName|사용자 식별자|  
|RequestType|가능한 값:<br /><br /> True = 구독 요청<br /><br /> False= 대화형 요청|  
|형식|렌더링 형식|  
|매개 변수|보고서 실행에 사용된 매개 변수 값|  
|TimeStart|보고서 처리 기간을 나타내는 시작 및 중지 시간|  
|TimeEnd||  
|TimeDataRetrieval|데이터 검색, 보고서 처리 및 보고서 렌더링에 걸린 시간(밀리초 단위)|  
|TimeProcessing||  
|TimeRendering||  
|원본|보고서 실행의 원본입니다. 가능한 값: (1=Live, 2=Cache, 3=Snapshot, 4=History, 5=Adhoc, 6=Session, 7=RDCE).|  
|상태|가능한 값: rsSuccess, rsProcessingAborted 또는 오류 코드입니다. 여러 오류가 발생한 경우 첫 번째 오류만 기록됩니다.|  
|ByteCount|렌더링된 보고서 크기(바이트)|  
|RowCount|쿼리에서 반환된 행 수|  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 추적 로그에 대한 Reporting Services 이벤트 설정&#40;ULS&#41;](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)   
 [Reporting Services 로그 파일 및 소스](../report-server/reporting-services-log-files-and-sources.md)   
 [오류 및 이벤트 참조&#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

---
title: "DQS 로그 파일에 대한 고급 설정 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log files,advanced settings
- dqs log files,advanced settings
ms.assetid: 1d565748-9759-425c-ae38-4d2032a86868
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5182c032b4a0c21358631df64f43dc16cdbd9ecf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="configure-advanced-settings-for-dqs-log-files"></a>DQS 로그 파일에 대한 고급 설정 구성
  이 항목에서는 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 및 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 로그 파일에 대해 로그 파일의 롤링 파일 크기 제한을 설정하거나, 이벤트의 타임스탬프 패턴을 설정하는 등 고급 설정을 구성하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  이러한 작업은 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]를 사용하여 수행할 수 없으며 고급 사용자 전용입니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
  
-   DQS_MAIN 데이터베이스에서 A_CONFIGURATION 테이블의 구성 설정을 수정하려면 Windows 사용자 계정이 SQL Server 인스턴스에서 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
-   [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 로깅 설정을 구성하려면 DQLog.Client.xml 파일을 수정할 컴퓨터에서 Administrators 그룹의 멤버로 로그온해야 합니다.  
  
##  <a name="DQSServer"></a> Data Quality 서버 로그 설정 구성  
 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 로그 설정은 DQS_MAIN 데이터베이스의 A_CONFIGURATION 테이블에서 **ServerLogging** 행의 **VALUE** 열에 XML 형식으로 나타납니다. 다음 SQL 쿼리를 실행하여 구성 정보를 볼 수 있습니다.  
  
```  
select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
```  
  
 로깅의 구성 설정을 변경하려면 **ServerLogging** 행의 **VALUE** [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 열에서 알맞은 정보를 업데이트해야 합니다. 이 예에서는 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 로그 설정을 업데이트하여 롤링 파일 크기 제한을 25000KB로 설정합니다(기본값은 20000KB).  
  
1.  Microsoft SQL Server Management Studio를 시작하고 적합한 SQL Server 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다.  
  
3.  쿼리 편집기 창에서 다음 SQL 문을 복사합니다.  
  
    ```  
    -- Begin the transaction.  
    BEGIN TRAN  
    GO  
    -- set the XML value field for the row with name=ServerLogging  
    update DQS_MAIN.dbo.A_CONFIGURATION   
    set VALUE='<configuration>  
      <configSections>  
        <section name="loggingConfiguration" type="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.LoggingSettings, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" />  
      </configSections>  
      <loggingConfiguration name="Logging Application Block" tracingEnabled="true" defaultCategory="" logWarningsWhenNoCategoriesMatch="true">  
        <listeners>  
          <add fileName="###REPLACE_THIS_WITH_SQL_SERVER_INSTANCE_LOG_FOLDER_NAME###DQServerLog.###REPLACE_THIS_WITH_SQL_CATALOG_NAME###.log" footer="" formatter="Custom Text Formatter" header="" rollFileExistsBehavior="Increment" rollInterval="None" rollSizeKB="25000" timeStampPattern="yyyy-MM-dd" listenerDataType="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.RollingFlatFileTraceListenerData, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" traceOutputOptions="None" filter="All" type="Microsoft.Practices.EnterpriseLibrary.Logging.TraceListeners.RollingFlatFileTraceListener, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Rolling Flat File Trace Listener" />  
        </listeners>  
        <formatters>  
          <add template="{timestamp(local)}|[{threadName}]|{dictionary({value}|)}{message}" type="Microsoft.Practices.EnterpriseLibrary.Logging.Formatters.TextFormatter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Custom Text Formatter" />  
        </formatters>  
        <logFilters>  
          <add enabled="true" type="Microsoft.Practices.EnterpriseLibrary.Logging.Filters.LogEnabledFilter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="LogEnabled Filter" />  
        </logFilters>  
        <categorySources />  
        <specialSources>  
          <allEvents switchValue="All" name="All Events" />  
          <notProcessed switchValue="All" name="Unprocessed Category" />  
          <errors switchValue="All" name="Logging Errors & Warnings">  
            <listeners>  
              <add name="Rolling Flat File Trace Listener" />  
            </listeners>  
          </errors>  
        </specialSources>  
      </loggingConfiguration>  
    </configuration>'  
    WHERE NAME='ServerLogging'  
    GO  
    -- check the result  
    select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
  
    -- Commit the transaction.  
    COMMIT TRAN  
  
    ```  
  
4.  F5 키를 눌러 문을 실행합니다. **결과** 창에서 문이 성공적으로 실행되었는지 확인합니다.  
  
5.  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 로깅 구성 변경 내용을 적용하려면 다음 Transact-SQL 문을 실행해야 합니다. 새 쿼리 편집기 창을 열고 다음 Transact-SQL 문을 붙여 넣습니다.  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    DECLARE @return_value int  
    EXEC @return_value = [internal_core].[RefreshLogSettings]  
    SELECT 'Return Value' = @return_value  
    GO  
  
    ```  
  
6.  F5 키를 눌러 문을 실행합니다. **결과** 창에서 문이 성공적으로 실행되었는지 확인합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 로깅 설정 구성이 동적으로 생성되어 DQS_MAIN.Log 파일에 저장됩니다. SQL Server의 기본 인스턴스를 설치한 경우 이 파일은 대개 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log에 있습니다. 그러나 이 파일에서 직접 변경한 내용은 유지되지 않고 DQS_MAIN 데이터베이스의 A_CONFIGURATION 테이블에 있는 구성 설정이 이 변경 내용을 덮어씁니다.  
  
##  <a name="DQSClient"></a> Data Quality 클라이언트 로그 설정 구성  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 로그 설정 구성 파일 DQLog.Client.xml은 대개 C:\Program Files\Microsoft SQL Server\130\Tools\Binn\DQ\config에 있습니다. XML 파일 내용은 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 로그 구성 설정에 대해 전에 수정한 XML 파일과 비슷합니다. [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 로그 설정을 구성하려면  
  
1.  XML 편집 도구나 메모장을 관리자로 실행합니다.  
  
2.  DQLog.Client.xml 파일을 도구나 메모장에서 엽니다.  
  
3.  필요한 사항을 변경하고 파일을 저장하여 새 로깅 변경 내용을 적용합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DQS 로그 파일에 대한 심각도 수준 구성](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)  
  
  


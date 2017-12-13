---
title: "Analysis Services의 작업 로그 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aa1db060-95dc-4198-8aeb-cffdda44b140
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 85a9806ca93e6b6216d8327d785803e1de19abde
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="log-operations-in-analysis-services"></a>Analysis Services의 로그 작업
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Analysis Services 인스턴스를 설치 하는 각 인스턴스에 대해 하나씩의 msmdsrv.log 파일에 서버 알림, 오류 및 경고를 기록 합니다. 관리자는 이 로그에서 루틴 및 비정상적 이벤트에 대한 정보를 참조합니다. 최신 릴리스에서는 더 많은 정보를 포함하도록 로깅이 향상되었습니다. 이제 로그 레코드에는 제품 버전과 버전 정보, 프로세서, 메모리, 연결, 차단 이벤트 등이 모두 포함되어 있습니다. 전체 변경 목록은 [로깅 개선 사항](http://support.microsoft.com/kb/2965035)에서 확인할 수 있습니다.  
  
 대부분의 관리자와 개발자는 기본 제공 로깅 기능 이외에 Analysis Services 커뮤니티에서 제공하는 도구를 함께 사용하여 서버 작업(예: **ASTrace**)에 대한 데이터를 수집합니다. 다운로드 링크는 [Microsoft SQL Server 커뮤니티 샘플: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/) 를 참조하세요.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [로그의 위치 및 유형](#bkmk_location)  
  
-   [로그 파일 구성 설정에 대한 일반 정보](#bkmk_general)  
  
-   [MSMDSRV 서비스 로그 파일](#bkmk_msmdsrv)  
  
-   [쿼리 로그](#bkmk_querylog)  
  
-   [미니 덤프(.mdmp) 파일](#bkmk_mdmp)  
  
-   [팁과 모범 사례](#bkmk_tips)  
  
> [!NOTE]  
>  로깅에 대한 정보를 찾는 경우 처리 및 쿼리 실행 경로를 보여주는 추적 작업에도 관심을 가질 수 있습니다. 임시 및 지속적인 추적(예: 큐브 액세스 감사)에 대한 추적 개체와 비행 레코더, SQL Server Profiler 및 xEvent를 최대한 활용하는 방법에 대한 권장 사항은 [Analysis Services 인스턴스 모니터](../../analysis-services/instances/monitor-an-analysis-services-instance.md)페이지의 링크를 통해 확인할 수 있습니다.  
  
##  <a name="bkmk_location"></a> 로그의 위치 및 유형  
 Analysis Services에서는 아래 설명된 로그를 제공합니다.  
  
|파일 이름 또는 위치|형식|사용 대상|기본적으로 설정|  
|---------------------------|----------|--------------|-------------------|  
|Msmdsrv.log|오류 로그|일상 모니터링 및 기본 문제 해결|예|  
|관계형 데이터베이스의 OlapQueryLog 테이블|쿼리 로그|사용 최적화 마법사에 대한 입력 수집|아니요|  
|SQLDmp\<guid >.mdmp 파일|충돌 및 예외|상세한 문제 해결|아니오|  
  
 이 항목에서 다루지 않는 추가 정보는 [Microsoft 지원의 초기 데이터 수집 팁](http://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)링크를 참조하세요.  
  
##  <a name="bkmk_general"></a> 로그 파일 구성 설정에 대한 일반 정보  
 각 로그에 대한 섹션은 \Program Files\Microsoft SQL Server\MSAS13.MSSQLSERVER\OLAP\Config 폴더의 msmdsrv.ini 서버 구성 파일에 있습니다. 파일 편집에 대한 지침은 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md) 을 참조하세요.  
  
 가능한 경우 Management Studio의 서버 속성 페이지에서 로깅 속성을 설정하는 것이 좋습니다. 하지만 일부 경우에 관리 도구에 표시되지 않는 설정을 구성하려면 msmdsrv.ini 파일을 직접 편집해야 합니다.  
  
 ![로그 설정을 보여주는 config 파일의 섹션](../../analysis-services/instances/media/ssas-logfilesettings.png "로그 설정을 보여주는 config 파일의 섹션")  
  
##  <a name="bkmk_msmdsrv"></a> MSMDSRV 서비스 로그 파일  
 Analysis Services에서는 \program files\Microsoft SQL Server\\<instance\>\Olap\Log에 있는 msmdsrv.log 파일에 서버 작업을 인스턴스별로 하나씩 기록합니다.  
  
 이 로그 파일은 각 서비스를 다시 시작하면 비워집니다. 이전 릴리스에서는 관리자가 로그 파일이 사용할 수 없을 정도로 커지기 전에 로그 파일을 플러시하기 위해 종종 서비스를 다시 시작했습니다. 이제 더 이상 그럴 필요가 없습니다. SQL Server 2012 SP2 이상에 도입된 구성 설정을 사용하면 로그 파일의 크기와 기록을 제어할 수 있습니다.  
  
-   **MaxFileSizeMB** 는 최대 로그 파일 크기(MB)를 지정합니다. 기본값은 256입니다. 유효한 대체 값은 양의 정수여야 합니다. **MaxFileSizeMB** 에 도달하면 Analysis Services에서 현재 파일의 이름을 msmdsrv{current timestamp}.log 파일로 변경하고 새 msmdsrv.log 파일을 시작합니다.  
  
-   **MaxNumberFiles** 는 이전 로그 파일의 보존 여부를 지정합니다. 기본값은 0(사용 안 함)입니다. 이 값을 양의 정수로 변경하면 여러 버전의 로그 파일을 유지할 수 있습니다. **MaxNumberFiles** 에 도달하면 Analysis Services는 이름의 타임스탬프가 가장 오래된 파일을 삭제합니다.  
  
 이러한 설정을 사용하려면 다음을 수행합니다.  
  
1.  msmdsrv.ini를 메모장에서 엽니다.  
  
2.  다음 두 줄을 복사합니다.  
  
    ```  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    ```  
  
3.  msmdsrv.ini의 Log 섹션에서 msmdsrv.log에 대한 파일 이름 아래에 두 줄을 붙여넣습니다. 두 설정을 모두 수동으로 추가해야 합니다. msmdsrv.ini 파일에 두 설정에 대한 자리 표시자가 없습니다.  
  
     변경된 구성 파일은 다음과 같이 표시됩니다.  
  
    ```  
    <Log>  
    <File>msmdsrv.log</File>  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    <FileBufferSize>0</FileBufferSize>  
  
    ```  
  
4.  제공된 값이 원하는 값과 다를 경우 값을 편집합니다.  
  
5.  파일을 저장합니다.  
  
6.  서비스를 다시 시작합니다.  
  
##  <a name="bkmk_querylog"></a> 쿼리 로그  
 쿼리 로그는 사용자의 MDX 또는 DAX 쿼리 활동을 기록하지 않는다는 점에서 다소 잘못된 명칭입니다. 그 대신 쿼리 로그는 Analysis Services에서 생성된 쿼리에 대한 데이터를 수집하며, 이 데이터는 이후에 사용 빈도 기반 최적화 마법사에서 데이터 입력으로 사용됩니다. 쿼리 로그에서 수집된 데이터는 분석에 직접 사용되지 않습니다. 특히, 데이터 집합은 데이터 집합의 일부가 쿼리에 포함되어 있음을 나타내는 0 또는 1로 구성된 비트 배열로 설명됩니다. 즉, 이 데이터는 마법사에 사용하기 위한 것입니다.  
  
 쿼리 모니터링 및 문제 해결을 위해 대부분의 개발자와 관리자는 **ASTrace**커뮤니티 도구를 사용하여 쿼리를 모니터링합니다. SQL Server Profiler, xEvents 또는 Analysis Services 추적을 사용할 수도 있습니다. 추적 관련 링크는 [Analysis Services 인스턴스 모니터](../../analysis-services/instances/monitor-an-analysis-services-instance.md) 를 참조하세요.  
  
 쿼리 로그는 언제 사용하나요? 사용 빈도 기반 최적화 마법사를 포함하는 쿼리 성능 튜닝 방법으로 쿼리 로그를 사용하는 것이 좋습니다. 이 기능을 사용하도록 설정하고, 이 기능을 지원하도록 데이터 구조를 만들고, 로그를 찾아서 채우도록 Analysis Services에서 사용되는 속성을 설정해야 쿼리 로그가 생성됩니다.  
  
 쿼리 로그를 사용하려면 다음 단계를 수행합니다.  
  
1.  쿼리 로그를 저장할 SQL Server 관계형 데이터베이스를 만듭니다.  
  
2.  Analysis Services 서비스 계정에 데이터베이스에 대한 권한을 부여합니다. 이 계정에는 테이블을 만들고, 테이블에 쓰고, 테이블에서 읽을 수 있는 권한이 필요합니다.  
  
3.  SQL Server Management Studio에서 **Analysis Services** | **속성** | **일반**을 마우스 오른쪽 단추로 클릭하고 **CreateQueryLogTable** 을 true로 설정합니다.  
  
4.  필요에 따라 쿼리를 다른 속도로 샘플링하거나 테이블에 다른 이름을 사용하려면 **QueryLogSampling** 또는 **QueryLogTableName** 을 변경합니다.  
  
 쿼리 로그 테이블을 만들려면 샘플링 요구 사항을 충족하도록 충분한 MDX 쿼리를 실행해야 합니다. 예를 들어 기본값 10을 유지할 경우 최소 10 개의 쿼리를 실행해야 테이블이 만들어집니다.  
  
 쿼리 로그 설정은 서버 전체에 적용됩니다. 지정한 설정은 이 서버에서 실행되는 모든 데이터베이스에서 사용됩니다.  
  
 ![Management Studio에서 로그 설정을 쿼리할](../../analysis-services/instances/media/ssas-querylogsettings.png "Management Studio에서 쿼리 로그 설정")  
  
 구성 설정을 지정한 후 MDX 쿼리를 여러 번 실행합니다. 샘플링을 10으로 설정한 경우 쿼리를 11번 실행하고 테이블이 만들어지는지 확인합니다. Management Studio에서 관계형 데이터베이스 엔진에 연결하고, 데이터베이스 폴더를 열고, **테이블** 폴더를 열고, **OlapQueryLog** 가 있는지 확인합니다. 테이블이 즉시 표시되지 않는 경우 폴더를 새로 고쳐서 내용 변경 사항을 지정합니다.  
  
 쿼리 로그에서 사용 빈도 기반 최적화 마법사에 대한 충분한 데이터를 누적하도록 허용합니다. 쿼리 볼륨이 순환적인 경우 데이터 집합을 표시하는 데 충분한 트래픽을 캡처합니다. 마법사를 실행하는 방법은 [사용 빈도 기반 최적화 마법사](https://msdn.microsoft.com/library/ms189706.aspx) 를 참조하세요.  
  
 쿼리 로그 구성에 대한 자세한 내용은 [Analysis Services 쿼리 로그 구성](http://technet.microsoft.com/library/Cc917676) 을 참조하세요. 이 백서는 오래 전에 작성되었지만 쿼리 로그 구성은 최신 릴리스에서 변경되지 않았으므로 포함된 정보는 여전히 적용됩니다.  
  
##  <a name="bkmk_mdmp"></a> 미니 덤프(.mdmp) 파일  
 덤프 파일은 비정상적 이벤트를 분석하는 데 사용되는 데이터를 캡처합니다. Analysis Services에서는 서버 충돌, 예외 및 일부 구성 오류에 응답하여 미니 덤프(.mdmp)를 자동으로 생성합니다. 기능을 사용하도록 설정해도 충돌 보고서를 자동으로 보내지 않습니다.  
  
 충돌 보고서는 Msmdsrv.ini 파일의 Exception 섹션을 통해 구성합니다. 이러한 설정은 메모리 덤프 파일 생성을 제어합니다. 다음 코드 조각은 기본값을 보여 줍니다.  
  
```  
<Exception>  
<CreateAndSendCrashReports>1</CreateAndSendCrashReports>  
<CrashReportsFolder/>  
<SQLDumperFlagsOn>0x0</SQLDumperFlagsOn>  
<SQLDumperFlagsOff>0x0</SQLDumperFlagsOff>  
<MiniDumpFlagsOn>0x0</MiniDumpFlagsOn>  
<MiniDumpFlagsOff>0x0</MiniDumpFlagsOff>  
<MinidumpErrorList>0xC1000000, 0xC1000001, 0xC102003F, 0xC1360054, 0xC1360055</MinidumpErrorList>  
<ExceptionHandlingMode>0</ExceptionHandlingMode>  
<CriticalErrorHandling>1</CriticalErrorHandling>  
<MaxExceptions>500</MaxExceptions>  
<MaxDuplicateDumps>1</MaxDuplicateDumps>  
</Exception>  
```  
  
 **충돌 보고서 구성**  
  
 Microsoft 지원에서 별도로 지시하지 않는 한 대부분의 관리자는 기본 설정을 사용합니다. [Analysis Services를 구성하여 메모리 덤프 파일을 생성하는 방법](http://support.microsoft.com/kb/919711)라는 오래된 기술 자료 문서는 덤프 파일을 구성하는 방법에 대한 지침을 제공하는 데 사용됩니다.  
  
 수정될 가능성이 가장 높은 구성 설정은 메모리 덤프 파일을 생성할지 여부를 결정하는 데 사용되는 **CreateAndSendCrashReports** 설정입니다.  
  
|Value|설명|  
|-----------|-----------------|  
|0|메모리 덤프 파일을 해제합니다. 예외 섹션 아래의 모든 다른 설정은 무시됩니다.|  
|1.|(기본값) 사용하도록 설정되지만, 메모리 덤프 파일을 보내지 않습니다.|  
|2|사용하도록 설정되고 오류 보고서를 Microsoft로 자동으로 보냅니다.|  
  
 **CrashReportsFolder** 는 덤프 파일의 위치입니다. 기본적으로 .mdmp 파일 및 연결된 로그 레코드는 \Olap\Log 폴더에 있습니다.  
  
 **SQLDumperFlagsOn** 은 전체 덤프를 생성하는 데 사용됩니다. 기본적으로 전체 덤프는 사용되지 않습니다. 이 속성을 **0x34**로 설정할 수 있습니다.  
  
 다음 링크는 자세한 배경 정보를 제공합니다.  
  
-   [미니 덤프를 사용하여 SQL Server 자세히 보기](http://blogs.msdn.com/b/sqlcat/archive/2009/09/11/looking-deeper-into-sql-server-using-minidumps.aspx)  
  
-   [사용자 모드 덤프 파일을 만드는 방법](http://support.microsoft.com/kb/931673)  
  
-   [Sqldumper.exe 유틸리티를 사용하여 SQL Server에서 덤프 파일을 생성하는 방법](http://support.microsoft.com/kb/917825)  
  
##  <a name="bkmk_tips"></a> 팁과 모범 사례  
 이 섹션에서는 이 문서 전체에서 언급되는 팁에 대해 간략하게 설명합니다.  
  
-   msmdsrv 로그 파일의 크기와 수를 제어하도록 msmdsrv.log 파일을 구성합니다. 설정은 기본적으로 사용되지 않으므로 설치 후 단계로 설정을 추가해야 합니다. 이 항목의 [MSMDSRV 서비스 로그 파일](#bkmk_msmdsrv) 을 참조하세요.  
  
-   서버 작업에 대한 정보를 가져오는 데 사용되는 리소스에 대한 자세한 내용은 Microsoft 고객 지원 서비스의 [초기 데이터 수집](http://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)블로그 게시물을 참조하세요.  
  
-   쿼리 로그 대신 ASTrace2012를 사용하여 큐브를 쿼리 중인 사용자에 대해 알아봅니다. 쿼리 로그는 일반적으로 사용 빈도 기반 최적화 마법사에 대한 입력을 제공하는 데 사용되며 쿼리 로그에 캡처되는 데이터는 읽거나 해석하기 쉽지 않습니다. ASTrace2012는 쿼리 작업을 캡처하는 데 널리 사용되는 커뮤니티 도구입니다. [Microsoft SQL Server 커뮤니티 샘플: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 인스턴스 관리](../../analysis-services/instances/analysis-services-instance-management.md)   
 [SQL Server Profiler로 Analysis Services 모니터링 소개](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)   
 [Analysis Services에서 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  

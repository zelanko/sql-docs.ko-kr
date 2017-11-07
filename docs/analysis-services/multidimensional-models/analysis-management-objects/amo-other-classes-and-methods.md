---
title: "AMO 다른 클래스와 메서드 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- restores [AMO]
- AMO, backup and restore
- capture logs [AMO]
- AmoException class [AMO]
- Analysis Management Objects, backup and restore
- assembly objects [AMO]
- traces [AMO]
- backups [AMO]
ms.assetid: 60ed5cfa-3a03-4161-8271-0a71a3ae363b
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aca3ce3e5c98db0c60ca2ae03d7de15283b28f6b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="amo-other-classes-and-methods"></a>AMO 기타 클래스 및 메서드
  이 섹션에서는 OLAP 또는 데이터 마이닝과 관련 되지 않은 하 고 관리 하거나 개체를 관리 하는 데 유용한 일반적인 클래스 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 이러한 클래스에서는 저장 프로시저, 추적, 예외, 백업 및 복원 등의 기능을 제공합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [어셈블리 개체](#Assembly)  
  
-   [Backup 및 Restore 메서드](#Backup)  
  
-   [추적 개체](#Traces)  
  
-   [CaptureLog 클래스 및 CaptureXML 특성](#CaptureLog)  
  
-   [AMOException 예외 클래스](#AMO)  
  
 다음 그림에서는 이 항목에 설명된 클래스의 관계를 보여 줍니다.  
  
 ![AMO 다른 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-otherclasses.gif "AMO 다른 클래스")  
  
##  <a name="Assembly"></a>어셈블리 개체  
 <xref:Microsoft.AnalysisServices.Assembly> 개체를 서버의 어셈블리 컬렉션에 추가한 다음 Update 메서드를 사용하여 서버로 업데이트하면 <xref:Microsoft.AnalysisServices.Assembly> 개체가 만들어집니다.  
  
 <xref:Microsoft.AnalysisServices.Assembly> 제거를 제거하려면 <xref:Microsoft.AnalysisServices.Assembly> 개체의 Drop 메서드를 사용하여 삭제해야 합니다. <xref:Microsoft.AnalysisServices.Assembly> 개체를 데이터베이스의 어셈블리 컬렉션에서 제거해도 어셈블리가 삭제되지는 않습니다. 응용 프로그램이 다음에 실행될 때까지 해당 어셈블리가 응용 프로그램에 표시되지 않을 뿐입니다.  
  
 메서드 및 사용할 수 있는 속성에 대 한 자세한 내용은 참조 <xref:Microsoft.AnalysisServices.Assembly> 에서 <xref:Microsoft.AnalysisServices> 합니다.  
  
> [!IMPORTANT]  
>  COM 어셈블리는 보안 위험을 내포할 수 있습니다. 이러한 위험 및 기타 고려 사항으로 인해 COM 어셈블리는 [!INCLUDE[ssASversion10](../../../includes/ssasversion10-md.md)]에서 더 이상 사용되지 않습니다. COM 어셈블리는 후속 릴리스에서 지원되지 않을 수 있습니다.  
  
##  <a name="Backup"></a>Backup 및 Restore 메서드  
 Backup 및 Restore는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스의 복사본을 만드는 작업과 복사본을 사용하여 데이터베이스를 복원하는 작업에 사용할 수 있는 메서드입니다. Backup 메서드는 <xref:Microsoft.AnalysisServices.Database> 개체에 속해 있으며, Restore 메서드는 <xref:Microsoft.AnalysisServices.Server> 개체에 속해 있습니다.  
  
 서버 및 데이터베이스 관리자만 데이터베이스 백업을 수행할 수 있습니다. 서버 관리자만 백업한 서버가 아닌 다른 서버에 데이터베이스를 복원할 수 있습니다. 데이터베이스 관리자는 덮어쓸 데이터베이스가 자신의 소유인 경우에만 기존 데이터베이스를 덮어써서 복원할 수 있습니다. 데이터베이스가 원래 보안 정의로 복원된 경우에는 복원 후 데이터베이스 관리자가 복원된 데이터베이스에 액세스하지 못하게 될 수도 있습니다.  
  
 데이터베이스 백업 파일의 확장명은 .abf여야 합니다.  
  
### <a name="backup-method"></a>Backup 메서드  
 데이터베이스를 백업하려면 백업 파일의 이름을 매개 변수로 사용하여 데이터베이스 개체의 Backup 메서드를 호출해야 합니다.  
  
##### <a name="default-values"></a>기본값:  
 AllowOverwrite =**false**  
  
 BackupRemotePartitions =**false**  
  
 보안 =**CopyAll**  
  
 ApplyCompression =**true**  
  
### <a name="restore-method"></a>Restore 메서드  
 데이터베이스를 서버에 복원하려면 백업 파일의 이름을 매개 변수로 사용하여 서버의 Restore 메서드를 호출해야 합니다.  
  
##### <a name="default-values"></a>기본값:  
 AllowOverwrite =**false**  
  
 DataSourceType =**원격**  
  
 보안 =**CopyAll**  
  
##### <a name="restrictions"></a>제한 사항  
  
1.  로컬 파티션은 원격 파티션으로 복원될 수 없습니다.  
  
2.  원격 파티션은 로컬 파티션으로 복원될 수 없지만 백업된 서버가 아닌 다른 서버에 복원될 수 있습니다.  
  
### <a name="common-parameters-and-properties-for-backup-and-restore-methods"></a>Backup 및 Restore 메서드의 공통 매개 변수 및 속성  
  
-   **파일** 으로/에서 파일을 백업 (UNC 이름)의 이름입니다.  
  
-   **위치** 과 같은 서버 관련 백업 정보를 지정할 **BackupFile**합니다. 이 통해 원격 데이터베이스에 대 한 별도 백업 파일을 지정할 수 있습니다.  
  
-   **DatasourceID** 원격 서버에 있는 하위 데이터베이스의 ID를 지정 합니다.  
  
-   **ConnectionString** 원격 서버가 변경 되었을 경우 원격 데이터 원본을 조정할 수 있습니다. ConnectionString이 있는 경우에는 항상 DatasourceID를 지정해야 합니다.  
  
-   **폴더** 폴더는 로컬 하드 드라이브의 파티션에 대 한 다시 매핑할 수 있습니다.  
  
-   **원래** 은 로컬 파티션에 대 한 원래 폴더입니다.  
  
-   **새** 해당 'Original' 기존 폴더에 저장 하는 데 사용 하는 로컬 파티션의 새 위치입니다.  
  
-   **암호**비어 있지 않은 서버에서 백업 파일을 암호화를 지정 하는 경우, 합니다.  
  
##  <a name="Traces"></a>추적 개체  
 추적은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스를 모니터링, 재생 및 관리하는 데 사용되는 프레임워크입니다. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]와 같은 클라이언트 응용 프로그램은 추적에 대해 구독하고 서버는 추적 정의에 지정된 대로 추적 이벤트를 다시 보냅니다.  
  
 각 이벤트는 이벤트 클래스에서 설명됩니다. 이벤트 클래스는 생성된 이벤트의 유형을 설명합니다. 이벤트 클래스에서 이벤트 하위 클래스는 더 세분화된 범주를 설명합니다. 각 이벤트에 대한 설명은 여러 열로 구성되어 있습니다. 추적 이벤트를 설명하는 열은 모든 이벤트에 대해 일관되며 SQL 추적 구조를 따릅니다. 각 열에 기록되는 정보는 이벤트 클래스에 따라 다를 수 있습니다. 즉, 미리 정의된 열 집합이 각 추적에 대해 정의되기는 하지만 열의 의미는 이벤트 클래스에 따라 다를 수 있습니다. 예를 들어, TextData 열은 모든 문 이벤트에 대해 원본 ASSL을 기록하는 데 사용됩니다.  
  
 추적 정의에는 동시에 추적할 이벤트 클래스가 하나 이상 포함될 수 있습니다. 각 이벤트 클래스에 대해 하나 이상의 데이터 열을 추적 정의에 추가할 수 있지만 전체 추적 열을 사용해서는 안 됩니다. 데이터베이스 관리자는 사용 가능한 열 중에서 추적에 포함할 열을 결정할 수 있습니다. 또한 추적에서 임의 열에 대한 필터 조건을 기반으로 선택적으로 이벤트 클래스를 추적할 수 있습니다.  
  
 추적을 시작 및 삭제할 수 있습니다. 동시에 여러 추적을 실행할 수 있습니다. 추적 이벤트는 라이브로 캡처할 수 있으며 나중에 분석하거나 재생하기 위해 파일로 저장할 수도 있습니다. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 추적 이벤트를 분석 및 재생하는 데 사용되는 도구입니다. 동일 추적으로부터 이벤트를 수신하기 위해 여러 연결을 사용할 수 있습니다.  
  
 추적은 서버 추적과 세션 추적이라는 두 그룹으로 나뉩니다. 서버 추적은 서버의 모든 이벤트를 알리는 반면 세션 추적은 현재 세션의 이벤트만을 알립니다.  
  
 서버의 추적 컬렉션에서 추적은 다음과 같은 방법으로 정의됩니다.  
  
1.  <xref:Microsoft.AnalysisServices.Trace> 개체를 만들고 추적 ID, 이름, 로그 파일 이름, 추가|덮어쓰기 등을 포함한 개체의 기본 데이터를 채웁니다.  
  
2.  모니터링할 이벤트를 추적 개체의 이벤트 컬렉션에 추가합니다. 각 이벤트에 대한 데이터 열이 추가됩니다.  
  
3.  불필요한 데이터 행을 제외하는 필터를 필터 컬렉션에 추가하여 설정합니다.  
  
4.  추적을 시작합니다. 추적을 만들었다고 해서 데이터 수집이 시작되지는 않습니다.  
  
5.  추적을 중지합니다.  
  
6.  [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]를 사용하여 추적 파일을 검토합니다.  
  
 세션 개체의 추적은 다음과 같은 방법으로 얻을 수 있습니다.  
  
1.  SessionTrace에 의해 응용 프로그램에 생성된 추적 이벤트를 처리할 함수를 정의합니다. 가능한 이벤트로는 OnEvent 및 Stopped 이벤트가 있습니다.  
  
2.  정의된 함수를 이벤트 처리기에 추가합니다.  
  
3.  세션 추적을 시작합니다.  
  
4.  프로세스를 수행합니다. 그러면 함수 처리기에서 이벤트를 캡처합니다.  
  
5.  세션 추적을 중지합니다.  
  
6.  응용 프로그램 실행을 계속합니다.  
  
##  <a name="CaptureLog"></a>CaptureLog 클래스 및 CaptureXML 특성  
 AMO에서 실행되는 모든 동작이 XMLA 메시지로 서버에 전송됩니다. AMO는 SOAP 헤더 없이 이러한 메시지를 모두 캡처할 수 있는 기능을 제공합니다. 자세한 내용은 참조 [AMO 클래스 소개](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)합니다. CaptureLog는 AMO에서 개체와 작업을 스크립팅하는 메커니즘이며, 개체와 작업은 XMLA로 스크립팅됩니다.  
  
 XML 캡처를 시작 하려면 CaptureXML 서버 개체 속성 설정 해야 **true**합니다. 그러면 서버로 전송되는 모든 동작이 CaptureLog 클래스에 캡처되지만 서버로 전송되지는 않습니다. CaptureLog는 캡처 로그를 지우는 데 사용되는 Clear 메서드를 가지고 있으므로 클래스로 간주됩니다.  
  
 로그를 읽기 위해 문자열 컬렉션을 가져와서 문자열을 반복합니다. 서버 개체 메서드 ConcatenateCaptureLog를 사용하여 모든 로그를 한 문자열로 연결할 수도 있습니다. ConcatenateCaptureLog에는 매개 변수 3개가 사용되며 그 중 2개는 필수입니다. 필요한 매개 변수는 *트랜잭션*, Boolean 형식 및 *병렬*, Boolean 형식입니다. 경우 *트랜잭션* 로 설정 된 **true**, 별도 트랜잭션으로 처리 되 고 각 명령 대신 단일 트랜잭션으로 XML 배치 파일이 만들 수 있는지 나타냅니다. 경우 *병렬* 로 설정 된 **true**, 기록 된 대로 배치 파일에서 모든 명령이 순차적으로 하는 대신 동시 실행에 대 한 기록 될 것을 나타냅니다.  
  
##  <a name="AMO"></a>AMOException 예외 클래스  
 AMOException 예외 클래스를 사용하여 AMO에서 throw된 예외를 응용 프로그램에서 쉽게 catch할 수 있습니다.  
  
 AMO는 다양한 문제가 발생할 때 예외를 throw합니다. 다음 표에서는 AMO에서 처리되는 예외의 종류를 보여 줍니다. 예외는 <xref:Microsoft.AnalysisServices.AmoException> 클래스에서 파생됩니다.  
  
|Exception|파생 위치|Description|  
|---------------|------------|-----------------|  
|<xref:Microsoft.AnalysisServices.AmoException>|기본 클래스|필수 부모 개체가 없거나 요청된 항목이 컬렉션에 없는 경우 응용 프로그램에서 이 예외가 발생합니다.|  
|<xref:Microsoft.AnalysisServices.OutOfSyncException>|AMOException에서 파생됨|AMO가 엔진과 동기화되어 있지 않고 AMO가 인식할 수 없는 개체 참조가 엔진에서 반환되는 경우 응용 프로그램에서 이 예외가 발생합니다.|  
|<xref:Microsoft.AnalysisServices.OperationException>|AMOException에서 파생됨|이 예외는 응용 프로그램에서 자주 발생하는 중요한 예외입니다. 이 예외에는 업데이트, 처리, 삭제 등의 잘못된 AMO 작업으로 인해 서버에서 보낸 오류에 대한 세부 사항이 포함됩니다.|  
|<xref:Microsoft.AnalysisServices.ResponseFormatException>|AMOException에서 파생됨|이 예외는 엔진이 AMO에서 인식되지 않는 형식의 메시지를 반환하는 경우에 발생합니다.|  
|<xref:Microsoft.AnalysisServices.ConnectionException>|AMOException에서 파생됨|이 예외는 Server.Connect를 사용하여 연결을 설정할 수 없는 경우 또는 AMO가 업데이트, 처리, 삭제 등의 작업을 위해 엔진과 통신 중일 때 연결이 끊어진 경우에 발생합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices>   
 [AMO 클래스 소개](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [논리적 아키텍처 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  


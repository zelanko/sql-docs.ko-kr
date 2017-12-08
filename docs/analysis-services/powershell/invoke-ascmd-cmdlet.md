---
title: "호출 ASCmd cmdlet | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2896b74a-3911-4b3f-89ab-bb375bdb34d8
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6e5d1fba56fd4cee4c736a583d8af2fe8ec6f986
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="invoke-ascmd-cmdlet"></a>Invoke-ASCmd cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  데이터베이스 관리자는 이 cmdlet을 사용하여 XMLA 스크립트, MDX(Multidimensional Expression), DMX(Data Mining Extension) 문 또는 TMSL(Tabular Model Scripting Language) 스크립트를 실행할 수 있습니다.  
  
 TMSL은 SQL Server 2016 Analysis Services 인스턴스의 테이블 형식 서버 모드에만 사용할 수 있습니다.  
  
 데이터베이스 또는 다른 개체를 만들려는 경우 이 cmdlet을 스크립트 입력 파일과 함께 사용합니다.  
  
## <a name="syntax"></a>구문  
 `Invoke-ASCmd –Query <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
 `Invoke-ASCmd –InputFile <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Invoke-ASCmd cmdlet은 입력 파일에 포함된 쿼리 또는 스크립트를 실행할 수 있습니다.  
  
 XMLA에 대해 지원되는 명령은 Alter, Backup, Batch, BeginTransaction, Cancel, ClearCache, CommitTransaction, Create, Delete, DesignAggregations, Drop, Insert, Lock, MergePartitions, NotifyTableChange, Process, Restore, RollbackTransaction, Statement(MDX 쿼리 및 DMX 문을 실행하는 데 사용됨), Subscribe, Synchronize, Unlock, Update, UpdateCells입니다.  
  
 TMSL의 경우에는 Alter, Create, Delete, MergePartitions, Process, Update 명령을 사용할 수 있습니다.  
  
 이 cmdlet은 –Credential 매개 변수를 지원하며, 이 매개 변수는 HTTP 액세스를 위해 Analysis Services 인스턴스를 구성한 경우 사용할 수 있습니다. –Credential 매개 변수는 Windows 사용자 ID를 제공하는 PSCredential 개체를 사용합니다. IIS는 Analysis Services에 연결할 때 이 사용자를 가장합니다. 스크립트를 실행하려면 ID에 Analysis Services 인스턴스에 대한 시스템 관리자 권한이 있어야 합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-query-string"></a>-쿼리 \<문자열 >  
 파일 대신 명령줄에서 실제 스크립트, 쿼리 또는 문을 직접 지정합니다. 쿼리를 파이프라인 입력으로 지정할 수도 있습니다. **Invoke-AsCmd** 를 사용하는 경우 **–InputFile** 또는 **–Query**매개 변수의 값을 지정해야 합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|True(ByValue)|  
|와일드카드 문자 허용|false|  
  
### <a name="-inputfile-string"></a>-InputFile \<문자열 >  
 XMLA 스크립트, MDX 쿼리, DMX 문 또는 JSON의 TMSL 스크립트가 포함된 파일을 식별합니다. **Invoke-AsCmd** 를 사용하는 경우 **–InputFile** 또는 **–Query**매개 변수의 값을 지정해야 합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-server-string"></a>-서버 \<문자열 >  
 cmdlet이 연결하고 실행할 Analysis Services 인스턴스를 지정합니다. 서버 이름을 제공하지 않으면 localhost에 연결됩니다. 기본 인스턴스의 경우에는 서버 이름만 지정합니다. 명명된 인스턴스의 경우에는 servername\instancename 형식을 사용합니다. HTTP 연결의 경우 http[s]://server[:port]/virtualdirectory/msmdpump.dll 형식을 사용합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|localhost|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-database-string"></a>-데이터베이스 \<문자열 >  
 MDX 쿼리 또는 DMX 문이 실행될 데이터베이스를 지정합니다. 데이터베이스 이름이 XMLA 스크립트에 포함되어 있으므로 cmdlet이 XMLA 스크립트를 실행할 때 데이터베이스 매개 변수는 무시됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 Windows 사용자 이름 및 암호를 제공하는 PSCredential 개체를 지정합니다. Analysis Services 인스턴스가 기본 인증을 사용하여 HTTP 액세스를 사용하도록 구성된 경우에만 이 매개 변수를 지정합니다. 통합 보안을 사용하는 네이티브 연결의 경우에는 이 매개 변수가 무시됩니다.  
  
 이 매개 변수가 있으면 해당 매개 변수가 제공하는 자격 증명이 연결 문자열에 추가됩니다. IIS는 Analysis Services에 연결할 때 이 사용자 ID를 가장합니다. 자격 증명을 지정하지 않으면 도구를 실행 중인 사용자의 기본 Windows 계정이 사용됩니다.  
  
 이 매개 변수를 사용하려면 먼저 Get-Credential을 사용하여 PSCredential 개체를 만들어 사용자 이름 및 암호를 지정합니다(예: `$Cred=Get-Credential “adventure-works\admin”`). 그런 다음 이 개체를 –Credential 매개 변수에 파이프할 수 있습니다 `(-Credential:$Cred`).  
  
   HTTP 액세스에 대한 자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하세요.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|True(ByValue)|  
|와일드카드 문자 허용|false|  
  
### <a name="-connectiontimeout-int"></a>-ConnectionTimeout \<int >  
 Analysis Services 인스턴스에 대한 연결 제한 시간을 나타내는 시간(초)을 지정합니다. 제한 시간 값은 0에서 65534 사이의 정수여야 합니다. 0을 지정하면 연결 시도 시간이 제한되지 않습니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|30|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-querytimeout-int"></a>-QueryTimeout \<int >  
 쿼리 제한 시간(초)을 지정합니다. 제한 시간 값을 지정하지 않으면 쿼리 시간이 제한되지 않습니다. 제한 시간은 1에서 65535 사이의 정수여야 합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|30|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-variable-string"></a>-변수 \<string >  
 추가 스크립팅 변수를 지정합니다. 각 변수는 이름 - 값 쌍입니다. 값에 공백이나 제어 문자가 있으면 해당 문자를 큰따옴표(")로 묶어야 합니다. 변수 및 해당 값을 여러 개 지정하려면 PowerShell 배열을 사용합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-tracefile-string"></a>-TraceFile \<문자열 >  
 XMLA 스크립트, MDX 쿼리 또는 DMX 문을 실행하는 동안 Analysis Services 추적 이벤트를 받는 파일을 식별합니다. 파일이 이미 있으면 해당 파일을 자동으로 덮어씁니다. 단, -TraceLevel:Duration 및 –TraceLevel:DurationResult 매개 변수 설정을 사용하여 만든 추적 파일은 예외입니다. 공백이 포함된 파일 이름은 큰따옴표(" ")로 묶어야 합니다. 파일 이름이 잘못된 경우 오류 메시지가 생성됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-tracefileformat-string"></a>-TraceFileFormat \<문자열 >  
 –TraceFile 매개 변수(지정한 경우)의 파일 형식을 지정합니다. 사용할 수 있는 옵션은 text 또는 csv입니다. 기본값은 "csv"입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|csv|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-tracefiledelimiter-string"></a>-TraceFileDelimiter \<문자열 >  
 추적 파일 형식으로 csv를 지정할 때 추적 파일 구분 기호로 사용할 문자를 지정합니다. 기본값은 |(파이프 또는 세로 막대)입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-tracetimeout-int"></a>-TraceTimeout \<int >  
 –TraceFile 매개 변수를 지정한 경우 추적을 끝낼 때까지 Analysis Services 엔진이 대기하는 시간(초)을 지정합니다. 지정한 기간 동안 추적 메시지가 기록되지 않으면 추적은 완료된 것으로 간주됩니다. 기본 추적 제한 시간 값은 5초입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|5|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-tracelevel-traceleveloption"></a>-TraceLevel \<TraceLevelOption >  
 추적 파일에 수집되고 기록되는 데이터 종류를 지정합니다. 사용할 수 있는 값은 High, Medium, Low, Duration 또는 DurationResult입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|높음|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer 및 -OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|PSObject|  
|출력|문자열|  
  
## <a name="example-1-xmla-input-file"></a>예 1(XMLA 입력 파일)  
  
```  
Invoke-ASCmd –InputFile:"C:\MyFolder\DiscoverConnections.xmla"  
```  
  
 이 명령은 서버의 활성 연결 목록을 반환하는 XMLA 스크립트를 실행합니다. DiscoverConnections.xmla 파일에는 다음 XMLA 스크립트가 포함됩니다.  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
<RequestType>DISCOVER_CONNECTIONS</RequestType>  
<Restrictions />  
   <Properties>  
      <PropertyList>  
         <Content>Data</Content>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="example-2-tmsl-input-file"></a>예 2(TMSL 입력 파일)  
 이 예는 스크립트가 TMSL(JSON)이며 SQL Server 2016의 테이블 형식 인스턴스가 필요하다는 점을 제외하면 첫 번째 예와 동일합니다. TMSL 스크립트는 SQL Server Management Studio에서 생성할 수 있습니다.  
  
 인스턴스가 여러 개인 경우 테이블 형식 인스턴스가 명명된 인스턴스이면 서버 이름을 설정해야 합니다.  
  
```  
Invoke-ASCmd –InputFile "C:\folder-name\T1200-NewDB.json" -Server "server-name\instance-name"  
```  
  
## <a name="example-3-query"></a>예3(쿼리)  
  
```  
Invoke-ASCmd -Database:"Adventure Works DW" -Query:"<Discover xmlns='urn:schemas-microsoft-com:xml analysis'><RequestType>DISCOVER_DATASOURCES</RequestType><Restrictions></Restrictions><Properties></Properties></Discover>"  
```  
  
 Discover XMLA 쿼리는 분석 서버가 사용할 수 있는 데이터 원본 및 해당 원본에 연결하는 데 필요한 정보를 반환합니다. 결과는 XML로 표시됩니다. 코드를 쉽게 확인하려는 경우 명령에 `| Out-file C:\Results\XMLAQueryOutput.xml` 을 추가하는 등의 방법으로 XML 파일에 출력을 파이프한 다음 구조화된 XML을 지원하는 브라우저나 기타 응용 프로그램에서 결과를 확인할 수 있습니다.  
  
  
  

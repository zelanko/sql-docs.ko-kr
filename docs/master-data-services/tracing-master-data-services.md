---
title: 추적(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: 45823fc8-723a-49f2-9a11-94d241245cfd
author: leolimsft
ms.author: lle
manager: erikre
ms.openlocfilehash: 054c6d8ea517bf3a2edd64622fc7385d8f9e24f6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705951"
---
# <a name="tracing-master-data-services"></a>추적(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Web.config 파일에는 다음과 같은 추적 섹션이 포함되어 있습니다. 이 섹션은 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
```  
<sources>  
      <!-- Adjust the switch value to control the types of messages that should be logged.   
           http://msdn.microsoft.com/library/system.diagnostics.sourcelevels  
           Use the a switchValue of Verbose to generate a full log. Please be aware that   
           the trace file can get quite large very quickly -->  
      <source name="MDS" switchType="System.Diagnostics.SourceSwitch" switchValue="Warning, ActivityTracing">  
        <listeners>  
          <!-- Set a directory path where the service account you chose while setting up Master Data Services has read and write privileges.  
               Default path is Logs in WebApplication folder, for example C:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication  
               New log file will be created every day or every 10 mb.  
               When directory size hits the 200mb limitation, the oldest file will be deleted.-->  
          <add name="FileTraceListener"  
               type="Microsoft.MasterDataServices.Core.Logging.FileTraceListener, Microsoft.MasterDataServices.Core"   
               initializeData="DirectoryPath = Logs; FileSizeInMb = 10; MaxDirectorySizeInMb = 200"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
  
```  
  
 기본 추적 동작은 다음과 같습니다.  
  
-   추적은 Warning 및 ActivityTracing 메시지에 대해 사용하도록 설정됩니다.  
  
     자세한 내용은 [SourceLevels 열거형](https://msdn.microsoft.com/library/system.diagnostics.sourcelevels)을 참조하세요.  
  
-   로그는 WebApplication 폴더 아래의 Logs 폴더에 저장됩니다. 기본 위치는 C:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication\Logs입니다.  
  
-   매일 10MB마다 파일이 생성됩니다.  
  
-   디렉터리 크기가 200MB가 되면 가장 오래된 로그가 삭제됩니다.  
  
-   로그 형식은 CSV입니다. 다음 표에서는 로그 형식에 대해 설명합니다.  
  
    |요소|설명|  
    |-------------|-----------------|  
    |Time|추적 항목이 생성된 시간입니다.|  
    |CorrelationID|요청마다 상관 관계 ID 하나가 할당됩니다. 하나의 요청에 의해 트리거되는 모든 추적은 같은 상관 관계 ID를 공유합니다.<br /><br /> UI에서 오류가 발생하면 오류 메시지에 상관 관계 ID가 표시됩니다.|  
    |연산|요청 작업 이름입니다. 웹 UI 요청의 경우 작업 이름은 URL입니다. API 요청의 경우 작업 이름은 서비스 이름입니다.|  
    |Level|이 추적 항목의 수준입니다.|  
    |메시지|추적의 메시지 본문입니다.|  
  
## <a name="external-resources"></a>외부 리소스  
 msdn.com의 블로그 게시물 [로깅 문제 해결 개선](http://go.microsoft.com/fwlink/p/?LinkId=615377)  
  
  

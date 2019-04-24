---
title: 보고서 서버 HTTP 로그 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- HTTP [Reporting Services]
ms.assetid: 6cc433b7-165c-4b16-9034-79256dd6735f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b4e7850cb0c66b6acbc7be54178cbc9ace27ce72
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59961109"
---
# <a name="report-server-http-log"></a>보고서 서버 HTTP 로그
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 HTTP 로그 파일은 보고서 서버에서 처리하는 모든 HTTP 요청 및 응답에 대한 기록을 유지합니다. 요청 오버플로 및 제한 시간 오류는 보고서 서버에 도달하지 않으므로 로그 파일에 기록되지 않습니다.  
  
 HTTP 로깅은 기본적으로 사용되지 않습니다. HTTP 로깅을 사용하려면 설치에서 이 기능을 사용하도록 **ReportingServicesService.exe.config** 구성 파일을 수정합니다.  
  
## <a name="viewing-log-information"></a>로그 정보 보기  
 로그는 ASCII 텍스트 파일입니다. 이 파일은 아무 텍스트 편집기에서 열어볼 수 있습니다. 보고서 서버 HTTP 로그 파일은 IIS의 W3C 확장 로그 파일에 해당하며 유사한 필드를 사용하므로 기존 IIS 로그 파일 뷰어를 사용하여 보고서 서버 HTTP 로그 파일을 읽을 수 있습니다. 다음 표에서는 HTTP 로그 파일에 대한 추가 정보를 제공합니다.  
  
|||  
|-|-|  
|**파일 이름**|기본적으로, 로그 파일 이름은<br /><br /> `ReportServerService_HTTP_<timestamp>.log.`<br /><br /> ReportingServicesService.exe.config 파일에서 HttpTraceFileName 특성을 수정하여 파일 이름의 접두사를 사용자 지정할 수 있습니다. 타임스탬프는 UTC(Coordinated Universal Time)를 기반으로 합니다.|  
|**파일 위치**|파일은 다음 위치에 기록됩니다.<br /><br /> `\Microsoft SQL Server\<SQL Server Instance>\Reporting Services\LogFiles`|  
|**파일 형식**|파일은 EN-US 형식이며 ASCII 텍스트 파일입니다.|  
|**파일 생성 및 보존**|HTTP 로그는 구성 파일에서 사용하도록 설정하고, 서비스를 다시 시작하고, 보고서 서버가 HTTP 요청을 처리한 후에 만들어집니다. 설정을 구성했지만 로그 파일이 표시되지 않을 경우 보고서를 열거나 보고서 관리자와 같은 보고서 서버 애플리케이션을 시작하여 해당 파일을 만들기 위한 HTTP 요청을 생성합니다.<br /><br /> 로그 파일의 새 인스턴스는 각 서비스 다시 시작 작업 및 보고서 서버에 대한 이후 HTTP 요청 후에 만들어집니다.<br /><br /> 기본적으로 추적 로그는 32MB로 제한되며 14일 후 삭제됩니다.|  
  
## <a name="configuration-settings-for-report-server-http-log"></a>보고서 서버 HTTP 로그에 대한 구성 설정  
 보고서 서버 HTTP 로그를 구성하려면 메모장을 사용하여 **ReportingServicesService.exe.config** 파일을 수정합니다. 구성 파일은 \Program Files\Microsoft SQL Server\MSSQL.n\Reporting Services\ReportServer\Bin 폴더에 있습니다.  
  
 HTTP 서버를 사용하려면 ReportingServicesService.exe.config 파일의 RStrace 섹션에 `http:4`를 추가합니다. 다른 모든 HTTP 로그 파일 항목은 선택 사항입니다. 다음 예에는 모든 설정이 포함되어 있으므로 RStrace 섹션에 전체 섹션을 붙여 넣은 다음 필요하지 않은 설정을 삭제할 수 있습니다.  
  
```  
   <RStrace>  
         <add name="FileName" value="ReportServerService_" />  
         <add name="FileSizeLimitMb" value="32" />  
         <add name="KeepFilesForDays" value="14" />  
         <add name="Prefix" value="tid, time" />  
         <add name="TraceListeners" value="debugwindow, file" />  
         <add name="TraceFileMode" value="unique" />  
         <add name="HttpTraceFileName" value="ReportServerService_HTTP_" />  
         <add name="HttpTraceSwitches" value="date,time, clientip,username,serverip,serverport,host,method,uristem,uriquery,protocolstatus,bytesreceived,timetaken,protocolversion,useragent,cookiereceived,cookiesent,referrer" />  
         <add name="Components" value="all:3,http:4" />  
   </RStrace>  
```  
  
## <a name="log-file-fields"></a>로그 파일 필드  
  다음 표에서는 로그에서 사용 가능한 필드를 설명합니다.   필드 목록은 구성 가능하므로 `HTTPTraceSwitches` 구성 설정을 통해 포함할 필드를 지정할 수 있습니다.  합니다 **기본** 포함될지 여부를 필드 로그 파일에 자동으로 지정 하지 않으면 열 지정 `HTTPTraceSwitches`합니다.  
  
|필드|Description|Default|  
|-----------|-----------------|-------------|  
|HttpTraceFileName|이 값은 선택 사항입니다. 기본값은 ReportServerServiceHTTP_입니다. 로그 파일을 중앙 위치에 저장하기 위해 서버 이름을 포함하는 경우와 같이 다른 파일 명명 규칙을 사용하려면 다른 값을 지정할 수 있습니다.|사용자 계정 컨트롤|  
|HTTPTraceSwitches|이 값은 선택 사항입니다. 이 값을 지정하면 로그 파일에 사용되는 필드를 쉼표로 구분된 형식으로 구성할 수 있습니다.|아니요|  
|Date|작업이 발생한 날짜입니다.|아니요|  
|Time|작업이 발생한 시간입니다.|아니요|  
|ClientIp|보고서 서버에 액세스하는 클라이언트의 IP 주소입니다.|사용자 계정 컨트롤|  
|UserName|보고서 서버에 액세스한 사용자의 이름입니다.|아니요|  
|ServerPort|연결에 사용되는 포트 번호입니다.|아니요|  
|Host|호스트 헤더의 내용입니다.|아니요|  
|메서드|클라이언트에서 호출된 동작 또는 SOAP 메서드입니다.|사용자 계정 컨트롤|  
|UriStem|액세스한 리소스입니다.|사용자 계정 컨트롤|  
|UriQuery|리소스에 액세스하는 데 사용된 쿼리입니다.|아니요|  
|ProtocolStatus|HTTP 상태 코드입니다.|사용자 계정 컨트롤|  
|BytesReceived|서버가 받은 바이트 수입니다.|아니요|  
|TimeTaken|네트워크 전송 시간을 제외하고 HTTP.SYS가 요청 데이터를 반환한 순간부터 서버가 마지막 보내기 작업을 마칠 때까지의 시간(밀리초)입니다.|아니요|  
|ProtocolVersion|클라이언트에 사용된 프로토콜 버전입니다.|아니요|  
|UserAgent|클라이언트에 사용된 브라우저 종류입니다.|아니요|  
|CookieReceived|서버가 받은 쿠키의 내용입니다.|아니요|  
|CookieSent|서버가 보낸 쿠키의 내용입니다.|아니요|  
|Referrer|클라이언트가 방문한 이전 사이트입니다.|아니요|  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 서비스 추적 로그](report-server-service-trace-log.md)   
 [Reporting Services 로그 파일 및 소스](../report-server/reporting-services-log-files-and-sources.md)   
 [오류 및 이벤트 참조&#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

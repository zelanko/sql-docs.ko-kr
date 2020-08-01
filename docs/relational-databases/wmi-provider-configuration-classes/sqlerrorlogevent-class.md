---
title: SqlErrorLogEvent 클래스
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 37f5dfbdc8b6d962d6bff91491142b9190818bb9
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442506"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent 클래스
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]
  지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일에서 이벤트를 보기 위한 속성을 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
class SQLErrorLogEvent   
{  
   stringFileName;  
   stringInstanceName;  
   datetimeLogDate;  
   stringMessage;  
   stringProcessInfo;  
};  
```  
  
## <a name="properties"></a>속성  
 SQLErrorLogEvent 클래스는 다음 속성을 정의 합니다.  
  
| 속성 | Description |
| -------- | ----------- |
|FileName|데이터 형식: **문자열**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 오류 로그 파일의 이름입니다.|  
|InstanceName|데이터 형식: **문자열**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> 한정자: Key<br /><br /> 로그 파일이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|LogDate|데이터 형식: **datetime**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> 한정자: Key<br /><br /> <br /><br /> 이벤트가 로그 파일에 기록된 날짜와 시간입니다.|  
|메시지|데이터 형식: **문자열**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 이벤트 메시지입니다.|  
|ProcessInfo|데이터 형식: **문자열**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 이벤트의 SPID(원본 서버 프로세스 ID)에 대한 정보입니다.|  
  
## <a name="remarks"></a>설명  
  
| Type | Name |
| ---- | ---- |
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|네임스페이스|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>예제  
 다음 예에서는 지정된 로그 파일에서 로깅된 모든 이벤트의 값을 검색하는 방법을 보여 줍니다. 예제를 실행 하려면을 \<*Instance_Name*> ' Instance1 '과 같은의 인스턴스 이름으로 바꾸고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ' File_Name '을 오류 로그 파일의 이름 (예: ' ')으로 바꿉니다.  
  
```  
on error resume next  
strComputer = "."  
Set objWMIService = GetObject("winmgmts:" _  
    & "{impersonationLevel=impersonate}!\\" _  
    & strComputer & "\root\MICROSOFT\SqlServer\ComputerManagement10")  
set logEvents = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogEvent WHERE InstanceName = '<Instance_Name>' AND FileName = 'File_Name'")  
  
For Each logEvent in logEvents  
WScript.Echo "Instance Name: " & logEvent.InstanceName & vbNewLine _  
    & "Log Date: " & logEvent.LogDate & vbNewLine _  
    & "Log File Name: " & logEvent.FileName & vbNewLine _  
    & "Process Info: " & logEvent.ProcessInfo & vbNewLine _  
    & "Message: " & logEvent.Message & vbNewLine _  
  
Next  
```  
  
## <a name="comments"></a>주석  
 *InstanceName* 또는 *FileName* 이 WQL 문에 제공 되지 않은 경우 쿼리는 기본 인스턴스와 현재 로그 파일에 대 한 정보를 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 예를 들어 다음 WQL 문은 기본 인스턴스(MSSQLSERVER)의 현재 로그 파일(ERRORLOG)에서 모든 로그 이벤트를 반환합니다.  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>보안  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]WMI를 통해 로그 파일에 연결 하려면 로컬 컴퓨터와 원격 컴퓨터 모두에 대 한 다음 권한이 있어야 합니다.  
  
-   **Root\Microsoft\SqlServer\ComputerManagement10** WMI 네임 스페이스에 대 한 읽기 액세스입니다. 기본적으로 모든 사용자는 계정 사용 권한으로 읽기 액세스합니다.  
  
-   오류 로그를 포함하는 폴더에 대한 읽기 권한. 기본적으로 오류 로그는 다음 경로에 있습니다. 여기서 *는를 \<*Drive> 설치한 드라이브를 나타내고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<*InstanceName*> 는 인스턴스의 이름입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     ** \<Drive> : Files\Microsoft SQL Server\MSSQL13** **. \<InstanceName> \MSSQL\Log**  
  
 방화벽을 통해 연결하는 경우 방화벽에 원격 대상 컴퓨터의 WMI에 대한 예외가 설정되어 있는지 확인합니다. 자세한 내용은 [Windows Vista부터 원격으로 WMI에 연결](https://go.microsoft.com/fwlink/?LinkId=178848)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SqlErrorLogFile 클래스](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [오프라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)  
  
  

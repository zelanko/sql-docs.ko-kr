---
title: SqlErrorLogEvent 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 65c2eb3758524788d0c65645d3b5736c930d58ac
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37204900"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent 클래스
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
 SQLErrorLogEvent 클래스에 다음 속성을 정의합니다.  
  
|||  
|-|-|  
|FileName|데이터 형식: `string`<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 오류 로그 파일의 이름입니다.|  
|InstanceName|데이터 형식: `string`<br /><br /> 액세스 형식: 읽기 전용<br /><br /> 한정자: Key<br /><br /> 로그 파일이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|LogDate|데이터 형식: `datetime`<br /><br /> 액세스 형식: 읽기 전용<br /><br /> 한정자: Key<br /><br /> <br /><br /> 이벤트가 로그 파일에 기록된 날짜와 시간입니다.|  
|메시지|데이터 형식: `string`<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 이벤트 메시지입니다.|  
|ProcessInfo|데이터 형식: `string`<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 이벤트의 SPID(원본 서버 프로세스 ID)에 대한 정보입니다.|  
  
## <a name="remarks"></a>Remarks  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Namespace|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>예제  
 다음 예에서는 지정된 로그 파일에서 로깅된 모든 이벤트의 값을 검색하는 방법을 보여 줍니다. 예제를 실행 하려면 대체 \< *Instance_Name*>의 인스턴스 이름을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 'Instance1' 등으로 바꿉니다 오류 로그 파일의 이름으로 'ERRORLOG.1')' 등입니다.  
  
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
 때 *InstanceName* 하거나 *FileName* 쿼리는 기본 인스턴스와 현재에 대 한 정보를 반환 하는 WQL 문에서 제공 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일입니다. 예를 들어 다음 WQL 문은 기본 인스턴스 (MSSQLSERVER)에서 현재 로그 파일 (ERRORLOG)에서 모든 로그 이벤트를 반환 됩니다.  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>보안  
 에 연결 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일 WMI를 통해 로컬 및 원격 컴퓨터에는 다음 권한이 있어야 합니다.  
  
-   에 대 한 읽기 액세스를 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 네임 스페이스입니다. 기본적으로 모든 사용자는 계정 사용 권한으로 읽기 액세스합니다.  
  
-   오류 로그를 포함하는 폴더에 대한 읽기 권한. 기본적으로 오류 로그는 다음 경로에 있습니다 (여기서 \< *드라이브 >* 설치한 드라이브를 나타내고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하 고 \< *InstanceName*>는 인스턴스의 이름을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<드라이브 >: \Program Files\Microsoft SQL Server\MSSQL12** **.\< N a m e > \MSSQL\Log**  
  
 방화벽을 통해 연결하는 경우 방화벽에 원격 대상 컴퓨터의 WMI에 대한 예외가 설정되어 있는지 확인합니다. 자세한 내용은 [WMI Remotely Starting with Windows Vista 연결할](http://go.microsoft.com/fwlink/?LinkId=178848)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SqlErrorLogFile 클래스](sqlerrorlogfile-class.md)   
 [오프라인 로그 파일 보기](../logs/view-offline-log-files.md)  
  
  

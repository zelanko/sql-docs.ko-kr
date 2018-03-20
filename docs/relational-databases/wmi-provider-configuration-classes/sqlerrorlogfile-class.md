---
title: "SqlErrorLogFile 클래스 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c02dbcc76ffc90f3a654b38e4ee23ea6cfac877e
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="sqlerrorlogfile-class"></a>SqlErrorLogFile 클래스
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일에 대한 정보를 보기 위한 속성을 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
class SQLErrorLogFile  
{  
   uint32ArchiveNumber;  
   stringInstanceName;  
   datetimeLastModified;  
   uint32LogFileSize;  
   stringName;  
  
};  
```  
  
## <a name="properties"></a>속성  
 SQLErrorLogFile 클래스는 다음 속성을 정의 합니다.  
  
|||  
|-|-|  
|ArchiveNumber|데이터 형식: **uint32**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 로그 파일에 대한 보관 파일 번호입니다.|  
|InstanceName|데이터 형식: **문자열**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> 한정자: Key<br /><br /> <br /><br /> 로그 파일이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|LastModified|데이터 형식: **날짜/시간**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 로그 파일이 마지막으로 수정된 날짜입니다.|  
|LogFileSize|데이터 형식: **uint32**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> <br /><br /> 로그 파일의 크기(바이트)입니다.|  
|이름|데이터 형식: **문자열**<br /><br /> 액세스 형식: 읽기 전용<br /><br /> 한정자: Key<br /><br /> <br /><br /> 로그 파일의 이름입니다.|  
  
## <a name="remarks"></a>주의  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|네임스페이스|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>예제  
 다음 예에서는 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일에 대한 정보를 검색합니다. 이 예제를 실행 하려면 대체 \< *Instance_Name*> 인스턴스의 예를 들어: 'Instance1' 이름으로 합니다.  
  
```  
on error resume next  
set strComputer = "."  
set objWMIService = GetObject("winmgmts:\\.\root\Microsoft\SqlServer\ComputerManagement10")  
set LogFiles = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogFile WHERE InstanceName = '<Instance_Name>'")  
  
For Each logFile in LogFiles  
  
WScript.Echo "Instance Name:  " & logFile.InstanceName & vbNewLine _  
    & "Log File Name:  " & logFile.Name & vbNewLine _  
    & "Archive Number: " & logFile.ArchiveNumber & vbNewLine _  
    & "Log File Size:  " & logFile.LogFileSize & " bytes" & vbNewLine _  
    & "Last Modified:  " & logFile.LastModified & vbNewLine _  
  
Next   
```  
  
## <a name="comments"></a>설명  
 때 *InstanceName* 쿼리는 기본 인스턴스에 대 한 정보를 반환 하는 WQL 문을 제공 되지 않았습니다. 예를 들어 다음 WQL 문은 기본 인스턴스(MSSQLSERVER)에서 모든 로그 파일에 대한 정보를 반환합니다.  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>보안  
 에 연결 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일 WMI를 통해 로컬 및 원격 컴퓨터 모두에 다음 권한이 있어야 합니다.  
  
-   에 대 한 읽기 액세스는 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 네임 스페이스입니다. 기본적으로 모든 사용자는 계정 사용 권한으로 읽기 액세스합니다.  
  
    > [!NOTE]  
    >  WMI 사용 권한을 확인 하는 방법에 대 한 내용은 항목의 보안 섹션을 참조 하십시오. [오프 라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)합니다.  
  
-   오류 로그를 포함하는 폴더에 대한 읽기 권한. 기본적으로 오류 로그는 다음 경로에 있습니다 (여기서 \< *드라이브 >* 설치한 드라이브를 나타내는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 \< *InstanceName*>은 인스턴스 이름을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<Drive>:\Program Files\Microsoft SQL Server\MSSQL11** **.\<InstanceName>\MSSQL\Log**  
  
 방화벽을 통해 연결하는 경우 방화벽에 원격 대상 컴퓨터의 WMI에 대한 예외가 설정되어 있는지 확인합니다. 자세한 내용은 참조 [WMI Remotely Starting with Windows Vista 연결할](http://go.microsoft.com/fwlink/?LinkId=178848)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SqlErrorLogEvent 클래스](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md)   
 [오프라인 로그 파일 보기](../../relational-databases/logs/view-offline-log-files.md)  
  
  

---
title: GenerateDatabaseRightsScript 메서드(WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- GenerateDatabaseRightsScript method
ms.assetid: f2e6dcc9-978f-4c2c-bafe-36c330247fd0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8714aee2b5bb33c84a1d9f11b626d3e21e06ed1f
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65570965"
---
# <a name="configurationsetting-method---generatedatabaserightsscript"></a>ConfigurationSetting 메서드 - GenerateDatabaseRightsScript
  보고서 서버 데이터베이스와 보고서 서버 실행에 필요한 기타 데이터베이스에 사용자 권한을 부여하는 데 사용할 수 있는 SQL 스크립트를 생성합니다. 호출자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 서버에 연결하여 해당 스크립트를 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Public Sub GenerateDatabaseRightsScript(ByVal UserName As String, _  
    ByVal DatabaseName As String, ByVal IsRemote As Boolean, _  
    ByVal IsWindowsUser As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseRightsScript(string UserName, string DatabaseName, bool IsRemote, bool IsWindowsUser, out string Script,   
out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>매개 변수  
 *UserName*  
 스크립트에서 권한을 부여할 사용자의 이름 또는 Windows SID(보안 식별자)입니다.  
  
 *DatabaseName*  
 스크립트에서 사용자에게 액세스가 허용되는 데이터베이스의 이름입니다.  
  
 *IsRemote*  
 데이터베이스가 보고서 서버에 대해 원격인지 여부를 나타내는 부울 값입니다.  
  
 *IsWindowsUser*  
 지정된 사용자 이름이 Windows 사용자인지 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자인지를 나타내는 부울 값입니다.  
  
 *스크립트*  
 [out] 생성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트가 들어 있는 문자열입니다.  
  
 *HRESULT*  
 [out] 호출의 성공 여부를 나타내는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드 호출의 성공 또는 실패를 나타내는 *HRESULT* 를 반환합니다. 0 값은 메서드 호출이 성공했음을 나타냅니다. 0 이외의 값은 오류가 발생했음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 *DatabaseName* 이 비어 있으면 *IsRemote* 는 무시되고 데이터베이스 이름에 보고서 서버 구성 파일 값이 사용됩니다.  
  
 *IsWindowsUser*가 **true**로 설정된 경우 *UserName*은 \<domain>\\<username\> 형식이어야 합니다.  
  
 *IsWindowsUser* 를 **true**로 설정하면 생성된 스크립트에서 보고서 서버 데이터베이스를 기본 데이터베이스로 설정하여 사용자에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 로그인 권한을 부여하고, 보고서 서버 데이터베이스, 보고서 서버 임시 데이터베이스, master 데이터베이스 및 MSDB 시스템 데이터베이스에 대한 **RSExec** 역할을 부여합니다.  
  
 *IsWindowsUser* 를 **true**로 설정하면 메서드에서 표준 Windows SID를 입력으로 사용합니다. 입력된 표준 Windows SID 또는 서비스 계정 이름은 사용자 이름 문자열로 변환됩니다. 데이터베이스가 로컬 데이터베이스인 경우 계정은 계정의 지역화된 올바른 표현으로 변환되고 원격 데이터베이스인 경우 계정은 컴퓨터 계정으로 표현됩니다.  
  
 다음 표에서는 변환된 계정과 해당 원격 표현을 보여 줍니다.  
  
|변환된 계정/SID|일반 이름|원격 이름|  
|---------------------------------------|-----------------|-----------------|  
|(S-1-5-18)|로컬 시스템|\<Domain>\\<ComputerName\>$|  
|.\LocalSystem|로컬 시스템|\<Domain>\\<ComputerName\>$|  
|ComputerName\LocalSystem|로컬 시스템|\<Domain>\\<ComputerName\>$|  
|LocalSystem|로컬 시스템|\<Domain>\\<ComputerName\>$|  
|(S-1-5-20)|네트워크 서비스|\<Domain>\\<ComputerName\>$|  
|NT AUTHORITY\NetworkService|네트워크 서비스|\<Domain>\\<ComputerName\>$|  
|(S-1-5-19)|로컬 서비스|오류 - 아래를 참조하십시오.|  
|NT AUTHORITY\LocalService|로컬 서비스|오류 - 아래를 참조하십시오.|  
  
 [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]에서 기본 제공 계정을 사용하고 있고 보고서 서버 데이터베이스가 원격이면 오류가 반환됩니다.  
  
 **LocalService** 기본 제공 계정이 지정되어 있고 보고서 서버 데이터베이스가 원격이면 오류가 반환됩니다.  
  
 *IsWindowsUser* 가 true이고 *UserName* 에 제공된 값을 변환해야 하는 경우, WMI 공급자는 보고서 서버 데이터베이스가 같은 컴퓨터에 있는지 또는 원격 컴퓨터에 있는지를 확인합니다. WMI 공급자는 로컬 설치 여부를 확인하기 위해 다음 값 목록에 대해 DatabaseServerName 속성을 평가합니다. 일치 항목이 있으면 로컬 데이터베이스이고, 그렇지 않으면 원격 데이터베이스입니다. 비교 시 대/소문자는 구분되지 않습니다.  
  
|DatabaseServerName 값|예제|  
|---------------------------------|-------------|  
|"."||  
|"(local)"||  
|"LOCAL"||  
|localhost||  
|\<Machinename>|testlab14|  
|\<MachineFQDN>|example.redmond.microsoft.com|  
|\<IPAddress>|180.012.345,678|  
  
 *IsWindowsUser* 를 **true**로 설정하면 WMI 공급자는 LookupAccountName을 호출하여 계정의 SID를 가져온 다음 LookupAccountSID를 호출하여 이름을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트로 가져옵니다. 이렇게 하면 사용되는 계정 이름이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유효성 검사를 통과합니다.  
  
 *IsWindowsUser* 를 **false**로 설정하면 생성된 스크립트에서 보고서 서버 데이터베이스, 보고서 서버 임시 데이터베이스 및 MSDB 데이터베이스에 대한 **RSExec** 역할을 부여합니다.  
  
 *IsWindowsUser* 를 **false**로 설정하면 SQL Server 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 있어야 스크립트를 성공적으로 실행할 수 있습니다.  
  
 보고서 서버에 보고서 서버 데이터베이스가 지정되어 있지 않은 경우 GrantRightsToDatabaseUser를 호출하면 오류가 반환됩니다.  
  
 생성된 스크립트는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 및 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]을 지원합니다.  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [MSReportServer_ConfigurationSetting 멤버](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

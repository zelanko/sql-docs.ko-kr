---
title: Backup-asdatabase cmdlet | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea4e93828aded76fd45ffe6bd279cba8397d8483
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036564"
---
# <a name="backup-asdatabase-cmdlet"></a>Backup-ASDatabase cmdlet
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Analysis Services 백업 파일(.abf)로 Analysis Services 다차원 또는 테이블 형식 데이터베이스 백업  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
## <a name="syntax"></a>구문  
 `Backup-ASDatabase [-BackupFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
 `Backup-ASDatabase –Database <Microsoft.AnalysisServices.Database> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Analysis Services 시스템 관리자가 다차원 또는 테이블 형식 데이터베이스를 백업 파일로 백업할 수 있도록 해 줍니다. 위치를 지정하지 않으면 설치 중 지정된 기본 백업 위치가 사용됩니다.  
  
 백업하는 파일을 암호화할 수 있습니다. –FilePassword를 사용하여 파일을 암호화할 수 있습니다. 나중에 파일을 복원하는 경우 파일을 암호화할 때 지정한 암호를 제공해야 합니다.  
  
 이 cmdlet은 –Credential 매개 변수를 지원하며, 이 매개 변수는 HTTP 액세스를 위해 Analysis Services 인스턴스를 구성한 경우 사용할 수 있습니다. –Credential 매개 변수는 Windows 사용자 ID를 제공하는 PSCredential 개체를 사용합니다. IIS는 Analysis Services에 연결할 때 이 사용자를 가장합니다. 백업을 수행하려면 ID에 Analysis Services 인스턴스에 대한 시스템 관리자 권한이 있어야 합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-backupfile-string"></a>-BackupFile \<문자열 >  
 백업 파일의 경로 및 이름을 지정합니다. 경로 없이 파일 이름만 지정하는 경우 기본 백업 위치가 사용됩니다. 이 매개 변수는 –Name 매개 변수가 지정된 경우에만 사용됩니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-name-string"></a>-Name \<string>  
 백업할 Analysis Services 데이터베이스를 지정합니다. 이름을 문자열로 전달하려면 –Database 매개 변수 또는 –Name 매개 변수를 사용하여 데이터베이스를 지정하면 됩니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 이름이 같은 백업 파일을 덮어씁니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-backupremotepartitions-switchparameter"></a>-BackupRemotePartitions \<SwitchParameter >  
 원격 파티션이 백업에 포함되는지 여부를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-applycompressionswitchparameter"></a>-ApplyCompression\<SwitchParameter >  
 백업 파일을 압축할지 여부를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-filepassword-securestring"></a>-FilePassword \<SecureString >  
 백업 파일 암호화에 사용할 암호를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-locations-microsoftanalysisservicesbackuplocation"></a>-위치 \<Microsoft.AnalysisServices.BackupLocation >  
 백업 파일을 저장할 위치를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
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
  
### <a name="-database-microsoftanalysisservicesdatabase"></a>-데이터베이스 \<Microsoft.AnalysisServices.Database >  
 백업할 Analysis Services 데이터베이스 개체를 지정합니다. -Database 매개 변수 또는 –Name 매개 변수를 사용하여 데이터베이스를 지정할 수 있습니다. 데이터베이스 이름을 파이프하려면 –Database를 사용합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<CommonParameters>  
 이 cmdlet은 공통 매개 변수 -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer 및 -OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|Microsoft.AnalysisServices.Database<br /><br /> 백업할 데이터베이스를 여러 개 파이프할 수 있습니다(예: 특정 인스턴스의 모든 데이터베이스 파이프).|  
|출력|없음|  
  
## <a name="example-1"></a>예제 1  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >backup-asdatabase awdb-20110930.abf “Adventure Works” -AllowOverwrite -ApplyCompression  
```  
  
 이 명령은 Adventure Works 데이터베이스를 기본 백업 위치에 .abf 파일로 백업합니다. 이름이 같은 기존 파일이 해당 위치에 있으면 이 파일을 덮어씁니다.  
  
## <a name="example-2"></a>예제 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >$AWDB = get-item “databases\Adventure Works”   
PS SQLSERVER:\SQLAS\Localhost\default >Backup-asdatabase –database:$AWDB –AllowOverwrite  
```  
  
 이 명령은 -Backupfile 및 -Name 대신 –Database를 사용합니다. 데이터베이스 이름을 cmdlet에 파이프하려면 –Database 매개 변수를 사용합니다.  
  
## <a name="example-3"></a>예제 3  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default\databases >dir * | backup-asdatabase  
```  
  
 이 명령은 로컬 서버에 모든 데이터베이스를 백업합니다.  
  
## <a name="example-4"></a>예제 4  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\Localhost\default > backup-asdatabase –backupfile test.abf –name contoso_retail –filepassword:$pwd server myremoteserver  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 1번 줄과 2번 줄은 파일을 암호화하는 데 사용되는 암호를 묻는 데 사용됩니다.  
  
 3번 줄에서는 원격 Analysis Services 서버의 Contoso_Retail 예제 데이터베이스를 원격 서버의 test.abf라는 이름의 Analysis Services 백업 파일로 백업합니다. 이 파일은 기본 인스턴스의 기본 백업 폴더에 저장됩니다.  
  
 4번 줄과 5번 줄은 암호를 제거합니다.  
  
  
  

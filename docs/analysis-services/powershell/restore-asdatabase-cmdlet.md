---
title: "Restore-asdatabase 등이 cmdlet | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 8ab7a2d0-679c-40e6-b9b9-042184b2dfc9
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 86894e5f3c0d438a5a97c45e3927e3996ee6a6ab
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="restore-asdatabase-cmdlet"></a>Restore-ASDatabase cmdlet
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Analysis Services 인스턴스에 다차원 또는 테이블 형식 데이터베이스 백업 파일 (.abf)을 복원합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
## <a name="syntax"></a>구문  
 `Restore-ASDatabase [-RestoreFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] Locations <Microsoft.AnalysisServices.RestoreLocation[]>] [-Security <Microsoft.AnalysisServices.RestoreSecurity>] [-Password <System.SecureString>] [-StorageLocation <System.string>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Analysis Services 시스템 관리자가 다차원 또는 테이블 형식 데이터베이스를 백업(.abf) 파일에서 로컬 또는 원격 서버 인스턴스로 복원할 수 있도록 해 줍니다. 복원하는 파일이 암호화되어 있는 경우 –FilePassword를 사용하여 파일의 암호를 해독하는 데 사용할 암호를 제공합니다.  
  
 이 cmdlet은 –Credential 매개 변수를 지원하며, 이 매개 변수는 HTTP 액세스를 위해 Analysis Services 인스턴스를 구성한 경우 사용할 수 있습니다. –Credential 매개 변수는 Windows 사용자 ID를 제공하는 PSCredential 개체를 사용합니다. IIS는 Analysis Services에 연결할 때 이 사용자를 가장합니다. 파일을 복원하려면 ID에 Analysis Services 인스턴스에 대한 시스템 관리자 권한이 있어야 합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-restorefile-string"></a>-RestoreFile \<문자열 >  
 복원할 파일의 경로 및 이름을 지정합니다. 경로 없이 파일 이름만 지정하는 경우 기본 백업 위치가 사용됩니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-name-string"></a>-이름 \<문자열 >  
 복원할 Analysis Services 데이터베이스를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 이름과 위치가 같은 데이터베이스를 덮어씁니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-locations-microsoftanalysisservicesrestorelocation"></a>-위치 \<Microsoft.AnalysisServices.RestoreLocation >  
 복원할 파티션의 원격 위치를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-security-microsoftanalysisservicesrestoresecurity"></a>-보안 \<Microsoft.AnalysisServices.RestoreSecurity >  
 복원 작업에 사용되는 보안 설정을 나타냅니다. 사용할 수 있는 값은 CopyAll, SkipMembership 및 IgnoreSecurity입니다. CopyAll은 역할 및 멤버 자격을 복원합니다. SkipMembership은 역할만 다시 만듭니다. IgnoreSecurity는 역할을 제외하고 데이터베이스를 복원합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-password-securestring"></a>-Password \<SecureString >  
 암호화된 백업 파일을 복원하는 데 사용할 암호를 지정합니다. 원래 파일을 암호화하는 데 사용된 암호를 지정해야 합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-storagelocation-string"></a>-StorageLocation \<문자열 >  
 데이터베이스 저장소 위치를 지정합니다. 파일 시스템에서 데이터베이스 파일의 위치가 여기에 해당합니다. 대상 인스턴스의 백업 폴더로 지정된 기본 위치를 사용하지 않으려면 이 매개 변수를 설정합니다.  
  
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
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer 및 -OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|System.string<br /><br /> 문자열 값을 cmdlet에 파이프할 수 있습니다.|  
|출력|없음|  
  
## <a name="example-1"></a>예 1  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase awtest.abf testawrestoredb –security:CopyAll  
```  
  
 이 명령은 로컬 백업 폴더에 있는 Analysis Services 백업 파일(awtest.abf)을 로컬 Analysis Services 기본 인스턴스로 복원합니다. 데이터베이스 이름은 지정하지 않아도 됩니다. 이 경우 데이터베이스 이름은 복원 작업의 일부로 지정됩니다. Adding –Security:CopyAll은 백업 데이터베이스에서 새로 복원된 데이터베이스로 역할 및 역할 멤버 자격을 채웁니다.  
  
## <a name="example-2"></a>예제 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile testdb.abf –name AWTEST2 –password:$pwd  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 1번 줄과 2번 줄은 파일을 암호화하는 데 사용된 암호를 묻는 데 사용됩니다.  
  
 3번 줄은 Analysis Services 기본 인스턴스의 로컬 백업 폴더에 있는 암호화된 Analysis Services 백업 파일(testdb.abf)을 복원합니다.  
  
 4번 줄과 5번 줄은 암호를 제거합니다.  
  
## <a name="example-3-remote-scenario"></a>예제 3(원격 시나리오)  
 이 예제에서는 파일 공유에서 Analysis Services의 원격 인스턴스로 로컬 백업 파일을 복원하는 방법을 보여 줍니다. 이 예제에서는 백업 파일은 Analysis Services의 기본 인스턴스 및 **ssas-aw-srv01** 이라는 컴퓨터에서 **internetsales**라는 데이터베이스로 복원됩니다.  
  
 백업 파일은 공용 읽기 액세스 권한이 있는 네트워크 공유에 있습니다. 원격 Analysis Services 인스턴스에는 파일에 대한 읽기 권한이 있어야 합니다. 파일 위치는 네트워크 공유(드라이브 없음)여야 합니다.  
  
 이 예제에서는 SQLAS 공급자를 사용하지 않습니다. cmdlet을 독립 실행형 명령으로 실행할 수 있습니다.  
  
```  
PS SQLSERVER:\> restore-asdatabase -restorefile "\\FileServer01\DBFiles\InternetSalesTabular.abf" -name "internetsales  
" -server "SSAS-AW-SRV01"  
```  
  
## <a name="example-4"></a>예제 4  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile “\\myremoteserver\backups\testdb.abf” –name Contoso_Retail –server myremoteserver –storagelocation “\\myremoteserver\restoreDBFiles”  
```  
  
 이 명령은 원격 백업 폴더에 있는 암호화된 Analysis Services 백업 파일(testdb.abf)을 원격 Analysis Services 기본 인스턴스에 복원합니다. –StorageLocation 매개 변수는 데이터베이스 파일을 기본 위치 이외의 위치에 저장할 때 사용합니다. 이 경우 restoreDBfiles라는 파일 공유에 저장됩니다.  
  

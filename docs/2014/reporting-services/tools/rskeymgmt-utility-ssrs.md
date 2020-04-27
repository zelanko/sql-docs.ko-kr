---
title: rskeymgmt 유틸리티(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- joining report server instances [SQL Server]
- report server scale-out deployments [Reporting Services]
- cryptography [Reporting Services]
- multiple report server instances
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], scale-out deployments
- encryption [Reporting Services]
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 53f1318d-bd2d-4c08-b19f-c8b698b5b3d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c9b5ca361cbfb5de42341fad8625f10d7ce3c2fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099804"
---
# <a name="rskeymgmt-utility-ssrs"></a>rskeymgmt 유틸리티(SSRS)
  중요한 보고서 서버 데이터를 무단 액세스로부터 보호하는 데 사용할 대칭 키를 추출, 복원, 생성 및 삭제합니다. 이 유틸리티를 사용하여 수평적 스케일 아웃 배포에서 보고서 서버 인스턴스를 결합할 수도 있습니다. *보고서 서버 수평적 스케일 아웃 배포* 란 하나의 보고서 서버 데이터베이스를 공유하는 여러 보고서 서버 인스턴스를 말합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
      rskeymgmt {-?}  
{-eextract}  
{-aapply}  
{-ddeleteall}  
{-srecreatekey}  
{-rremoveinstancekey}  
{-jjoinfarm}  
{-iinstance}  
{-ffile}  
{-pencryptionpassword}  
{-mremotecomputer}  
{-ninstancenameofremotecomputer}  
{-uadministratoruseraccount}  
{-vadministratorpassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>인수  
 **-?**  
 **rskeymgmt** 인수의 구문을 표시합니다.  
  
 **-e**  
 파일로 복사할 수 있도록 보고서 서버 인스턴스의 데이터를 암호화 및 해독하는 데 사용할 대칭 키를 추출합니다.  
  
 이 인수는 값을 가지지 않습니다. 그러나 압축 풀기를 완료하려면 명령줄에 추가 인수를 포함해야 합니다. 지정해야 할 인수에는 `-f` 및 `-p` 인수가 있습니다.  
  
 **-a**  
 기존 대칭 키를 암호로 보호된 백업 파일에 제공한 복사본으로 바꿉니다. 대칭 키의 모든 인스턴스가 업데이트됩니다.  
  
 이 인수는 값을 가지지 않습니다. 그러나 적용된 키가 포함된 파일을 선택하려면 명령줄에 추가 인수를 포함해야 합니다. 지정할 수 있는 인수에는 `-f` 및 `-p` 인수가 있습니다.  
  
 **-d**  
 모든 대칭 키 인스턴스를 삭제하고 보고서 서버 데이터베이스에서 암호화된 모든 데이터를 삭제합니다. 이 인수는 값을 가지지 않습니다.  
  
 `-s`  
 새 대칭 키를 생성하고 이 키를 사용하여 암호화된 모든 내용을 다시 암호화합니다. 대칭 키의 모든 인스턴스가 다시 생성됩니다.  
  
 `-j`  
 로컬 보고서 서버 인스턴스에서 사용하는 보고서 서버 데이터베이스를 공유하도록 원격 보고서 서버 인스턴스를 구성합니다.  
  
 **-r**  *installationID*  
 특정 보고서 서버 인스턴스에 대한 대칭 키 정보를 제거합니다. 이에 따라 수평적 스케일 아웃 배포에서 보고서 서버도 제거됩니다. *installationID* 는 RSReportserver.config 파일에 포함된 GUID 값입니다.  
  
 `-f`  *파일과*  
 대칭 키의 백업 복사본을 저장하는 파일의 정규화된 경로를 지정합니다.  
  
 **rskeymgmt -e**의 경우 대칭 키가 지정한 파일에 기록됩니다.  
  
 **rskeymgmt -a**의 경우 파일에 저장된 대칭 키 값이 보고서 서버 인스턴스에 적용됩니다.  
  
 `-p`  *password*  
 `-f`의 경우 필수 인수입니다. 대칭 키를 백업하거나 적용하는 데 사용할 암호를 지정합니다. 이 값은 비워 둘 수 없습니다.  
  
 `-i`  
 로컬 보고서 서버 인스턴스를 지정합니다. 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 보고서 서버를 설치한 경우 이 인수는 옵션입니다. `-i`의 기본값은 MSSQLSERVER입니다. 보고서 서버를 명명된 인스턴스로 설치한 경우 `-i`이 필요합니다.  
  
 `-m`  
 보고서 서버 수평적 스케일 아웃 배포에 결합하는 보고서 서버 인스턴스를 호스팅하는 원격 컴퓨터의 이름을 지정합니다. 네트워크에서 식별할 수 있는 컴퓨터 이름을 사용합니다.  
  
 `-n`  
 원격 컴퓨터의 보고서 서버 인스턴스 이름을 지정합니다. 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 보고서 서버를 설치한 경우 이 인수는 옵션입니다. `-n`의 기본값은 MSSQLSERVER입니다. 보고서 서버를 명명된 인스턴스로 설치한 경우 `-n`이 필요합니다.  
  
 `-u`  *useraccount*  
 수평적 스케일 아웃 배포에 결합하는 원격 컴퓨터의 관리자 계정을 지정합니다. 계정을 지정하지 않으면 현재 사용자의 자격 증명이 사용됩니다.  
  
 `-v`  *password*  
 `-u`의 경우 필수 인수입니다. 수평적 스케일 아웃 배포에 결합할 원격 컴퓨터의 관리자 계정 암호를 지정합니다.  
  
 **-t**  *trace*  
 추적 로그에 오류 메시지를 출력합니다. 이 인수는 값을 가지지 않습니다. 자세한 내용은 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 이 도구를 실행하려면 로컬 관리자 권한이 있어야 하며 보고서 서버를 호스팅하는 컴퓨터에서 로컬로 실행해야 합니다. rskeymgmt 유틸리티는 로컬 보고서 서버 Windows 인스턴스에 사용할 수 있습니다. 이 유틸리티는 보고서 서버 Windows 서비스의 원격 인스턴스에 연결할 수 없으므로 원격 보고서 서버 인스턴스의 암호화 키를 관리하는 데 사용할 수 없습니다.  
  
> [!NOTE]  
>  `-u` 및 `-v` 인수를 사용하는 경우 원격 컴퓨터에 대해 관리자 권한이 있는 계정을 지정해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **rskeymgmt**를 사용하는 방법을 보여 줍니다. 다음 예에서는 암호화 키를 추출, 복원 및 삭제하는 방법과 보고서 서버 수평적 스케일 아웃 배포를 구성하는 방법을 보여 줍니다.  
  
#### <a name="extracting-encryption-keys"></a>암호화 키 추출  
 이 예에서는 암호화 키의 백업 복사본을 만들고 플로피 디스크의 암호로 보호된 파일에 저장하는 방법을 보여 줍니다. 보고서 서버를 명명된 인스턴스로 설치한 경우 `-i` 인수를 추가합니다.  
  
```  
rskeymgmt -e -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="restoring-encryption-keys"></a>암호화 키 복원  
 이 예에서는 암호화 키를 바꾸는 방법을 보여 줍니다. 암호화 키의 백업 복사본 위치와 이 파일의 잠금을 해제하는 암호를 지정해야 합니다.  
  
```  
rskeymgmt -a -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="deleting-encryption-keys-and-encrypted-content"></a>암호화 키 및 암호화된 내용 삭제  
 이 예에서는 보고서 서버에 저장된 모든 암호화 키를 삭제하는 방법을 보여 줍니다. 보고서 서버 수평적 스케일 아웃 배포로 설치한 경우 이 배포에 포함된 모든 보고서 서버 인스턴스의 암호화 키가 삭제됩니다. 암호화 키를 삭제하면 보고서 서버 데이터베이스에서 암호화된 기존 값도 삭제됩니다. 암호화된 내용에 대한 자세한 내용은 [암호화된 보고서 서버 데이터 저장&#40;SSRS Configuration Manager&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)를 참조하세요.  
  
```  
rskeymgmt -d  
```  
  
#### <a name="joining-a-remote-report-server-named-instance-to-a-scale-out-deployment"></a>원격 보고서 서버의 명명된 인스턴스를 수평적 확장 배포에 결합  
 이 예에서는 원격 컴퓨터에 설치된 보고서 서버 인스턴스를 보고서 서버 수평적 스케일 아웃 배포에 추가하는 방법을 보여 줍니다. 공유되는 데이터베이스를 사용하도록 이미 구성된 컴퓨터 중 하나에서 명령을 실행해야 합니다. 명령 인수는 수평적 스케일 아웃 배포에 포함할 원격 보고서 서버 인스턴스를 지정합니다.  
  
```  
rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
```  
  
> [!NOTE]  
>  보고서 서버 수평적 스케일 아웃 배포란 여러 보고서 서버 인스턴스가 같은 보고서 서버 데이터베이스를 공유하는 배포 모델을 말합니다. 보고서 서버 데이터베이스에 대칭 키를 저장하는 모든 보고서 서버 인스턴스에서 이 데이터베이스를 사용할 수 있습니다. 예를 들어 보고서 서버 데이터베이스에 3개의 보고서 서버 인스턴스에 대한 키 정보가 포함된 경우 세 인스턴스는 모두 같은 수평적 스케일 아웃 배포의 멤버로 간주됩니다.  
  
#### <a name="joining-report-server-instances-on-the-same-computer"></a>같은 컴퓨터에서 보고서 서버 인스턴스 조인  
 같은 컴퓨터에 설치된 여러 보고서 서버 인스턴스에서 스케일 아웃 배포를 만들 수 있습니다. 로컬로 설치된 보고서 서버 인스턴스를 조인하는 경우에는 `-u` 및 `-v` 인수를 설정하지 마십시오. `-u` 및 `-v` 인수는 원격 컴퓨터에서 인스턴스를 조인하는 경우에만 사용됩니다. 로컬인 경우 이러한 인수를 지정하면 "로컬 연결에 대해 사용자 자격 증명을 사용할 수 없습니다" 오류가 발생합니다.  
  
 다음 예에서는 여러 로컬 인스턴스를 사용하여 스케일 아웃 배포를 만드는 구문을 보여 줍니다. 이 예에서 <`initializedinstance`>는 보고서 서버 데이터베이스를 사용 하도록 이미 초기화 된 인스턴스의 이름이 고,> <`newinstance` 은 배포에 추가 하려는 인스턴스의 이름입니다.  
  
```  
rskeymgmt -j -i <initializedinstance> -m <computer name> -n <newinstance>  
```  
  
#### <a name="removing-encryption-keys-for-a-single-report-server-in-a-scale-out-deployment"></a>수평적 확장 배포에서 단일 보고서 서버의 암호화 키 제거  
 이 예에서는 보고서 서버 수평적 스케일 아웃 배포에서 단일 보고서 서버의 암호화 키를 제거하는 방법을 보여 줍니다. 이 키는 보고서 서버 데이터베이스에서 제거됩니다. 보고서 서버 인스턴스의 키가 제거되면 이 보고서 서버 인스턴스에서 데이터베이스의 암호화된 데이터에 더 이상 액세스할 수 없으며 수평적 스케일 아웃 배포에서 효과적으로 제거됩니다.  
  
 스케일 아웃 배포에서 보고서 서버 인스턴스를 제거하려면 설치 ID를 지정해야 합니다. 설치 ID는 암호화 키를 제거하려는 보고서 서버 인스턴스의 RSReportserver.config 파일에 저장된 GUID입니다. 수평적 스케일 아웃 배포에서 제거할 컴퓨터에서 다음 명령을 실행해야 합니다. 보고서 서버를 명명된 인스턴스로 설치한 경우 `-i` 인수를 사용하여 인스턴스를 지정합니다. 자세한 내용은 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
```  
rskeymgmt -r <installationID>  
```  
  
## <a name="file-location"></a>파일 위치  
 Rskeymgmt는 ** \< *drive*>: fileFiles\Microsoft SQL Server\110\Tools\Binn** 또는 ** \< *drive*>: filefiles (x86) \Microsoft sql Server\110\Tools\Binn**에 있습니다. 파일 시스템의 모든 폴더에서 유틸리티를 실행할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 보고서 서버는 저장된 자격 증명과 연결 정보를 암호화합니다. 데이터를 암호화하는 데 공개 키와 대칭 키가 사용됩니다. 보고서 서버를 실행하려면 보고서 서버 데이터베이스에 유효한 키가 있어야 합니다. **rskeymgmt** 를 사용하여 키를 백업, 삭제 또는 복원할 수 있습니다. 키를 복원할 수 없을 경우 이 도구는 더 이상 사용할 수 없는 암호화된 내용을 삭제하는 방법을 제공합니다.  
  
 **rskeymgmt** 유틸리티를 사용하여 설치하는 동안 또는 초기화하는 동안 정의되는 키 집합을 관리할 수 있습니다. 이 유틸리티는 원격 프로시저 호출(RPC) 엔드포인트를 통해 로컬 보고서 서버 Windows 서비스에 연결합니다. 이 유틸리티가 올바르게 작동하려면 보고서 서버 Windows 서비스가 실행 중이어야 합니다.  
  
 암호화 키에 대한 자세한 내용은 [암호화 키 구성 및 관리&#40;SSRS Configuration Manager&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md) 및 [보고서 서버 초기화&#40;SSRS Configuration Manager&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SSRS Configuration Manager 기본 모드 보고서 서버 스케일 아웃 배포 &#40;구성&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [SSRS&#41;&#40;보고서 서버 명령 프롬프트 유틸리티](report-server-command-prompt-utilities-ssrs.md)   
 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  

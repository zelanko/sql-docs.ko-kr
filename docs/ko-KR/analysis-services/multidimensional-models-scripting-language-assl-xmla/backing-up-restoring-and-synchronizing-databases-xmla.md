---
title: 백업, 복원, 데이터베이스 및 동기화 (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6a7b9d3c850052cf1d6a4548764482a287bf671c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>데이터베이스 백업, 복원 및 동기화(XMLA)
  XML for Analysis에는 데이터베이스를 백업, 복원 및 동기화하는 세 개의 명령이 있습니다.  
  
-   [백업](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) 명령은 백업는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 사용 하 여 데이터베이스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일 (.abf)로 섹션에 설명 된 대로 [데이터베이스 백업](#backing_up_databases)합니다.  
  
-   [복원](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 복원 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 섹션에 설명 된 대로.abf 파일에서 데이터베이스 [데이터베이스 복원](#restoring_databases)합니다.  
  
-   [동기화](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 명령 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 섹션에 설명 된 대로 데이터와 다른 데이터베이스의 메타 데이터 데이터베이스 [데이터베이스 동기화](#synchronizing_databases)합니다.  
  
##  <a name="backing_up_databases"></a> 데이터베이스 백업  
 앞에서 언급 된 **백업** 명령에서는 지정 된 백업 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 백업 파일입니다. **백업** 명령에는 데이터베이스를 백업할 수를 지정할 수 있는 다양 한 속성을 사용 하 고, 보안 정의 및 백업할 원격 파티션을 백업 하는 방법에 백업 파일입니다.  
  
> [!IMPORTANT]  
>  Analysis Services 서비스 계정에는 각 파일에 대해 지정한 백업 위치에 쓸 수 있는 권한이 있어야 합니다. 또한 사용자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 관리자 역할이나 백업할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버를 가지고 있어야 합니다.  
  
### <a name="specifying-the-database-and-backup-file"></a>데이터베이스 및 백업 파일 지정  
 설정 하면 데이터베이스를 백업할 수를 지정 하려면는 [개체](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) 의 속성은 **백업** 명령입니다. **개체** 속성에는 데이터베이스에 대 한 개체 식별자 있어야 합니다. 그렇지 않으면 오류가 발생 합니다.  
  
 설정 하면 생성 되 고 백업 프로세스에서 사용 되는 파일을 지정 하려면는 [파일](../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md) 의 속성은 **백업** 명령입니다. **파일** 속성은 만들 백업 파일에 대 한 UNC 경로 및 파일 이름으로 설정 합니다.  
  
 백업에 사용할 파일을 지정하는 것 외에도 지정된 백업 파일에 대해 다음과 같은 옵션을 설정할 수 있습니다.  
  
-   설정 하는 경우는 [AllowOverwrite](../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md) 속성을 true로는 **백업** 명령은 지정 된 파일이 이미 있는 경우 백업 파일을 덮어씁니다. 설정 하는 경우는 **AllowOverwrite** 속성을 false로 지정 된 백업 파일이 이미 있으면 오류가 발생 합니다.  
  
-   설정 하는 경우는 [ApplyCompression](../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md) 속성을 true로 백업 파일의 파일을 만든 후 압축 됩니다.  
  
-   설정 하는 경우는 [암호](../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md) 속성을 비어 있지 않은 값을 백업 파일 지정된 된 암호를 사용 하 여 암호화 됩니다.  
  
    > [!IMPORTANT]  
    >  경우 **ApplyCompression** 및 **암호** 지정 되지 않은, 백업 파일은 일반 텍스트로 연결 문자열에는 포함 된 사용자 이름 및 암호를 저장 합니다. 일반 텍스트로 저장된 데이터는 검색될 수 있으므로 보안 향상된을 위해 사용 하 여는 **ApplyCompression** 및 **암호** 설정을 둘 다에 압축 하 고 백업 파일을 암호화 합니다.  
  
### <a name="backing-up-security-settings"></a>보안 설정 백업  
 [보안](../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md) 속성 결정 여부는 **백업** 명령에 정의 된 역할 및 권한과 같은 보안 정의를 백업는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다. **보안** 속성 Windows 사용자 계정 및 그룹 보안 정의의 멤버로 정의 된 백업 파일에 포함할지 여부도 결정 합니다.  
  
 값은 **보안** 속성은 다음 표에 나열 된 문자열 중 하나로 제한 합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|*SkipMembership*|백업 파일에 보안 정의는 포함되지만 멤버 정보는 제외됩니다.|  
|*CopyAll*|백업 파일에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|백업 파일에서 보안 정의가 제외됩니다.|  
  
### <a name="backing-up-remote-partitions"></a>원격 파티션 백업  
 원격 파티션을 백업 하려면는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 설정 데이터베이스는 [BackupRemotePartitions](../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md) 속성은 **백업** true로 명령을 합니다. 이 설정을 사용 하면는 **백업** 명령을 데이터베이스에 대 한 원격 파티션을 저장 하는 데 사용 되는 각 원격 데이터 원본에 대 한 원격 백업 파일을 만듭니다.  
  
 백업할 각 원격 데이터 원본에 대 한 포함 하 여 해당 백업 파일을 지정할 수 있습니다는 [위치](../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) 요소에는 [위치](../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md) 의 속성은 **백업** 명령입니다. **위치** 요소에는 해당 **파일** 원격 백업 파일의 UNC 경로 및 파일 이름으로 설정 하는 속성 및 해당 [DataSourceID](../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md) 속성의 식별자로 설정 데이터베이스에 정의 된 원격 데이터 원본입니다.  
  
##  <a name="restoring_databases"></a> 데이터베이스 복원  
 **복원** 명령은 지정 된 복원 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일에서 데이터베이스입니다. **복원** 명령에 데이터베이스를 복원할 백업 파일을 사용 하 고 보안 정의 저장할 원격 파티션 및 재배치에서 복원 하는 방법을 지정할 수 있는 다양 한 속성이 ROLAP (관계형 OLAP) 개체입니다.  
  
> [!IMPORTANT]  
>  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
### <a name="specifying-the-database-and-backup-file"></a>데이터베이스 및 백업 파일 지정  
 **DatabaseName** 의 속성은 **복원** 명령에는 데이터베이스에 대 한 개체 식별자 있어야 합니다. 그렇지 않으면 오류가 발생 합니다. 지정한 데이터베이스가 이미 있는 경우는 **AllowOverwrite** 속성에서 기존 데이터베이스를 덮어쓸지 여부를 결정 합니다. 경우는 **AllowOverwrite** 속성을 false로 설정 되 고 지정한 데이터베이스가 이미 있으면 오류가 발생 합니다.  
  
 설정 해야는 **파일** 의 속성은 **복원** 지정된 된 데이터베이스에 복원할 백업 파일에 대 한 UNC 경로 및 파일 이름으로 명령을 합니다. 설정할 수도 있습니다는 **암호** 지정된 된 백업 파일에 대 한 속성입니다. 경우는 **암호** 속성이 비어 있지 않은 값으로 설정 되어 있으면 지정 된 암호를 사용 하 여 백업 파일이 해독 됩니다. 백업 파일이 암호화되지 않았거나 지정된 암호가 백업 파일을 암호화하는 데 사용된 암호와 일치하지 않으면 오류가 발생합니다.  
  
### <a name="restoring-security-settings"></a>보안 설정 복원  
 **보안** 속성 결정 여부는 **복원** 명령은 역할 및에 정의 된 권한과 같은 보안 정의 복원는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다. **보안** 속성 결정 여부는 **복원** 명령에는 Windows 사용자 계정 및 복원 프로세스의 일부로 보안 정의의 멤버로 정의 된 그룹이 포함 됩니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SkipMembership*|데이터베이스에 보안 정의는 포함되지만 멤버 정보는 제외됩니다.|  
|*CopyAll*|데이터베이스에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|데이터베이스에서 보안 정의가 제외됩니다.|  
  
### <a name="restoring-remote-partitions"></a>원격 파티션 복원  
 이전 하는 동안 만들어진 각 원격 백업 파일에 대 한 **백업** 명령을 포함 하 여 연결 된 해당 원격 파티션을 복원할 수는 **위치** 요소에는 **위치**의 속성은 **복원** 명령입니다. [DataSourceType](../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md) 각 속성이 **위치** 요소를 제외 하거나로 명시적으로 설정 해야 *원격*합니다.  
  
 지정 된 각 작업에 대 한 **위치** 요소는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 연결에 지정 된 원격 데이터 소스는 **DataSourceID** 원격 백업 파일에 정의 된 파티션을 복원 하는 속성 에 지정 된 된 **파일** 속성입니다. 외에는 **DataSourceID** 및 **파일** 속성을 다음 속성을 각각에 대해 사용할 수 있는 **위치** 원격 파티션을 복원 하는 데 사용 되는 요소:  
  
-   에 지정 된 원격 데이터 원본에 대 한 연결 문자열을 재정의 하려면 **DataSourceID**를 설정할 수 있습니다는 **ConnectionString** 속성의는 **위치** 요소를 한 다른 연결 문자열입니다. **복원** 명령에 포함 되는 연결 문자열을 사용 하 여 다음 됩니다는 **ConnectionString** 속성입니다. 경우 **ConnectionString** 를 지정 하지 않으면는 **복원** 명령은 지정 된 원격 데이터 원본에 대 한 백업 파일에 저장 된 연결 문자열을 사용 합니다. 사용할 수는 **ConnectionString** 설정을 원격 파티션을 다른 원격 인스턴스로 이동할 수 있습니다. 그러나 사용할 수 없습니다는 **ConnectionString** 설정이 복원된 된 데이터베이스가 들어 있는 동일한 인스턴스에 원격 파티션을 복원할 수 있습니다. 즉, 사용할 수 없습니다는 **ConnectionString** 속성 로컬 파티션에 원격 파티션을 만들을 합니다.  
  
-   원격 데이터 원본의 원격 파티션을 저장 하는 데 사용 각 원래 폴더에 대해 지정할 수 있습니다는 [폴더](../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) 요소를 원래 폴더에 저장 된 모든 원격 파티션을 복원할 새 폴더를 나타냅니다. 경우는 **폴더** 요소를 지정 하지 않으면는 **복원** 명령은 원격 백업 파일에 포함 된 원격 파티션에 대해 지정 된 원래 폴더를 사용 합니다.  
  
### <a name="relocating-rolap-objects"></a>ROLAP 개체 재배치  
 **복원** 집계 또는 데이터 등의 정보는 기본 관계형 데이터 원본에서 테이블로 저장 되므로 ROLAP 저장소를 사용 하는 개체에 대 한 명령으로 복원할 수 없습니다. 하지만 ROLAP 개체의 메타데이터는 복원할 수 있습니다. ROLAP 개체에 대 한 메타 데이터를 복원 하는 **복원** 명령에서는 관계형 데이터 원본에서 테이블 구조를 다시 만듭니다.  
  
 사용할 수는 **위치** 요소에는 **복원** ROLAP 개체 재배치 하는 명령입니다. 각 **위치** 데이터 원본을 재배치 하는 데 사용 되는 요소는 **DataSourceType** 속성으로 명시적으로 설정 되어 있어야 *로컬*합니다. 설정 해야 할 수도 있습니다는 **ConnectionString** 의 속성은 **위치** 새 위치의 연결 문자열로 요소입니다. 복원 되는 동안는 **복원** 명령으로 식별 되는 데이터 소스에 대 한 연결 문자열을 대체는 **DataSourceID** 의 속성은 **위치** 요소 값으로는 **ConnectionString** 의 속성은 **위치** 요소입니다.  
  
##  <a name="synchronizing_databases"></a> 데이터베이스 동기화  
 **동기화** 데이터와 메타 데이터의 지정 된 명령 동기화 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다른 데이터베이스와 데이터베이스입니다. **동기화** 명령에 다양 한 속성이 원본 데이터베이스를 지정할 수 있는 보안 정의 동기화 할 원격 파티션 및 ROLAP 개체의 동기화를 동기화 하는 방법입니다.  
  
> [!NOTE]  
>  **동기화** 된 서버 관리자와 데이터베이스 관리자만 명령을 실행할 수 있습니다. 원본 데이터베이스와 대상 데이터베이스의 데이터베이스 호환성 수준이 같아야 합니다.  
  
### <a name="specifying-the-source-database"></a>원본 데이터베이스 지정  
 [소스](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) 의 속성은 **동기화** 두 속성을 포함 하는 명령 **ConnectionString** 및 **개체**합니다. **ConnectionString** 원본 데이터베이스를 포함 하는 인스턴스의 연결 문자열을 포함 하는 속성 및 **개체** 속성 원본 데이터베이스에 대 한 개체 식별자를 포함 합니다.  
  
 대상 데이터베이스는 세션에 대 한 현재 데이터베이스의 **동기화** 명령 실행 합니다.  
  
 경우는 **ApplyCompression** 속성은 **동기화** 명령을 설정 되어 소스에서 전송 되는 정보를 true로 데이터베이스를 대상 데이터베이스에 전송 되기 전에 압축 합니다.  
  
### <a name="synchronizing-security-settings"></a>보안 설정 동기화  
 [SynchronizeSecurity](../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md) 속성 결정 여부는 **동기화** 명령은 역할 및 원본 데이터베이스에 정의 된 권한과 같은 보안 정의 동기화 합니다. **SynchronizeSecurity** 속성 결정 여부는 **동기화 할** 명령은 Windows 사용자 계정 및 보안 정의의 멤버로 정의 된 그룹을 포함 합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SkipMembership*|대상 데이터베이스에 보안 정의만 포함되고 멤버 정보는 제외됩니다.|  
|*CopyAll*|대상 데이터베이스에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|대상 데이터베이스에서 보안 정의가 제외됩니다.|  
  
### <a name="synchronizing-remote-partitions"></a>원격 파티션 동기화  
 원본 데이터베이스에 있는 각 원격 데이터 원본에 대해 동기화 할 수 있습니다 각 연결 된 원격 파티션을 포함 하 여 한 **위치** 요소에는 **위치** 의 속성은  **동기화** 명령입니다. 각 **위치** 요소는 **DataSourceType** 속성을 제외 하거나로 명시적으로 설정 해야 *원격*합니다.  
  
 정의 하 고 대상 데이터베이스에 원격 데이터 원본에 연결 된 **동기화** 명령은에 정의 된 연결 문자열을 사용 하 여는 **ConnectionString** 속성은 **위치**  요소입니다. **동기화** 명령을 사용 하 여 다음의 **DataSourceID** 속성은 **위치** 동기화 할 원격 파티션을 식별 하는 요소입니다. **동기화**명령은에 지정 된 원격 데이터 원본의 원격 파티션을 동기화는 **DataSourceID** 는 에지정된원격데이터원본과원본데이터베이스에대한속성 **DataSourceID** 대상 데이터베이스의 속성입니다.  
  
 원본 데이터베이스에 원격 데이터 원본의 원격 파티션을 저장 하는 데 사용 각 원래 폴더에 대해 지정할 수도 있습니다는 **폴더** 요소에는 **위치** 요소입니다. **폴더** 요소는 원격 데이터 원본의 원래 폴더에 저장 된 모든 원격 파티션을 동기화 할 대상 데이터베이스에 대 한 새 폴더를 나타냅니다. 경우는 **폴더** 요소가 지정 되지 않은 Synchronize 명령에서는 원본 데이터베이스에 포함 된 원격 파티션에 대해 지정 된 원래 폴더입니다.  
  
### <a name="synchronizing-rolap-objects"></a>ROLAP 개체 동기화  
 **동기화** 명령 집계 또는 이러한 정보는 기본 관계형 데이터 원본에서 테이블로 저장 되므로 ROLAP 저장소를 사용 하는 개체에 대 한 데이터를 동기화 할 수 없습니다. 하지만 ROLAP 개체의 메타데이터는 동기화할 수 있습니다. 메타 데이터를 동기화 하는 **동기화** 명령 관계형 데이터 원본에서 테이블 구조를 다시 만듭니다.  
  
 사용할 수는 **위치** ROLAP 개체를 동기화 하는 동기화 명령의 요소입니다. 각 **위치** 데이터 원본을 재배치 하는 데 사용 되는 요소는 **DataSourceType** 속성으로 명시적으로 설정 되어 있어야 *로컬*합니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 설정 해야 할 수도 있습니다는 **ConnectionString** 의 속성은 **위치** 새 위치의 연결 문자열로 요소입니다. 동기화 하는 동안는 **동기화** 명령으로 식별 되는 데이터 소스에 대 한 연결 문자열을 대체는 **DataSourceID** 의 속성은 **위치** 값을 가진 요소가 **ConnectionString** 의 속성은 **위치** 요소입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 & #40; 백업 XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [요소 & #40; 복원 XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [요소 & #40; 동기화 XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Analysis Services 데이터베이스 백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  

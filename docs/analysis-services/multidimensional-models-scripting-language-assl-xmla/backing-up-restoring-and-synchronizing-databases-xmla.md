---
title: 백업, 복원, 데이터베이스 및 동기화 (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19d311a07eb11f1c5119a3c20d7536b5a2986b49
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145938"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>데이터베이스 백업, 복원 및 동기화(XMLA)
  XML for Analysis에는 데이터베이스를 백업, 복원 및 동기화하는 세 개의 명령이 있습니다.  
  
-   합니다 [백업](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) 명령은 백업를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 사용 하 여 데이터베이스를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일 (.abf)로 섹션에 설명 된 대로 [데이터베이스 백업](#backing_up_databases)합니다.  
  
-   합니다 [복원](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) 명령를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 섹션에 설명 된 대로.abf 파일에서 데이터베이스 [Restoring](#restoring_databases)합니다.  
  
-   합니다 [동기화](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) 명령 동기화 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 섹션에 설명 된 대로 데이터 및 다른 데이터베이스의 메타 데이터를 사용 하 여 데이터베이스 [동기화 데이터베이스](#synchronizing_databases)합니다.  
  
##  <a name="backing_up_databases"></a> 데이터베이스 백업  
 앞서 언급 했 듯이 합니다 **백업** 명령에서는 지정 된 백업 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 백업 파일입니다. 합니다 **백업** 명령에 다양 한 속성이 데이터베이스를 백업할 수를 지정할 수 있는 백업 파일을 사용 하 고 보안 정 및 백업할 원격 파티션을 백업 하는 방법입니다.  
  
> [!IMPORTANT]  
>  Analysis Services 서비스 계정에는 각 파일에 대해 지정한 백업 위치에 쓸 수 있는 권한이 있어야 합니다. 또한 사용자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 관리자 역할이나 백업할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버를 가지고 있어야 합니다.  
  
### <a name="specifying-the-database-and-backup-file"></a>데이터베이스 및 백업 파일 지정  
 설정한 백업할 데이터베이스를 지정 하려면 합니다 [개체](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 의 속성을 **백업** 명령. 합니다 **개체** 속성을 데이터베이스에 대 한 개체 식별자가 있어야 하거나 오류가 발생 합니다.  
  
 설정한 만들어지고 백업 프로세스에서 사용 하는 파일을 지정 하려면 합니다 [파일](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla) 의 속성을 **백업** 명령. 합니다 **파일** 만들 백업 파일에 대 한 UNC 경로 및 파일 이름으로 속성을 설정 해야 합니다.  
  
 백업에 사용할 파일을 지정하는 것 외에도 지정된 백업 파일에 대해 다음과 같은 옵션을 설정할 수 있습니다.  
  
-   설정 하는 경우는 [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla) 속성을 true로 합니다 **백업** 명령은 지정 된 파일이 이미 있는 경우 백업 파일을 덮어씁니다. 설정한 경우에 **AllowOverwrite** 속성을 false로 지정된 된 백업 파일이 이미 있으면 오류가 발생 합니다.  
  
-   설정한 경우에 [ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla) 속성을 true로 백업 파일의 파일을 만든 후 압축 됩니다.  
  
-   설정한 경우에 [암호](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla) 속성 백업 파일을 모든 비어 있지 않은 값을 지정 된 암호를 사용 하 여 암호화 됩니다.  
  
    > [!IMPORTANT]  
    >  하는 경우 **ApplyCompression** 하 고 **암호** 속성 지정 되지 않은, 일반 텍스트로 연결 문자열에 포함 된 된 사용자 이름 및 암호가 백업 파일을 저장 합니다. 일반 텍스트로 저장된 데이터는 검색될 수 있으므로 향상 된 보안을 사용 합니다 **ApplyCompression** 및 **암호** 둘 다에 압축 설정과 백업 파일을 암호화 합니다.  
  
### <a name="backing-up-security-settings"></a>보안 설정 백업  
 [보안](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) 속성에 따라 결정 하는지 여부를 합니다 **백업** 명령에 정의 된 역할 및 권한과 같은 보안 정의 백업는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스. 합니다 **보안** 속성 Windows 사용자 계정 및 그룹 보안 정의의 멤버로 정의 된 백업 파일을 포함할지 여부도 결정 합니다.  
  
 값을 **보안** 속성은 다음 표에 나열 된 문자열 중 하나로 제한 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SkipMembership*|백업 파일에 보안 정의는 포함되지만 멤버 정보는 제외됩니다.|  
|*CopyAll*|백업 파일에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|백업 파일에서 보안 정의가 제외됩니다.|  
  
### <a name="backing-up-remote-partitions"></a>원격 파티션 백업  
 원격 파티션을 백업할를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 설정한 데이터베이스를 [BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla) 의 속성을 **백업** 로 명령을 합니다. 이 설정을 사용 하면 합니다 **백업** 명령을 데이터베이스에 대 한 원격 파티션을 저장 하는 데 사용 되는 각 원격 데이터 원본에 대 한 원격 백업 파일을 만듭니다.  
  
 백업할 각 원격 데이터 원본에 대해 해당 백업 파일을 포함 하 여 지정할 수 있습니다는 [위치](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla) 요소에는 [위치](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla) 속성을 **백업** 명령입니다. 합니다 **위치** 요소에는 해당 **파일** 원격 백업 파일의 UNC 경로 및 파일 이름으로 설정 하는 속성 및 해당 [DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceid-element-xmla) 속성의 식별자로 설정 데이터베이스에 정의 된 원격 데이터 원본입니다.  
  
##  <a name="restoring_databases"></a> 데이터베이스 복원  
 합니다 **복원** 명령은 지정 된 복원 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일에서 데이터베이스입니다. 합니다 **복원** 명령에는 복원할 데이터베이스, 백업 파일을 사용 하 고 보안 정의 저장할 원격 파티션 및 재배치를 복원 하는 방법을 지정할 수 있는 다양 한 속성이 ROLAP (관계형 OLAP) 개체입니다.  
  
> [!IMPORTANT]  
>  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
### <a name="specifying-the-database-and-backup-file"></a>데이터베이스 및 백업 파일 지정  
 합니다 **DatabaseName** 의 속성을 **복원** 명령을 데이터베이스에 대 한 개체 식별자가 있어야 하거나 오류가 발생 합니다. 지정한 데이터베이스가 이미 있는 경우는 **AllowOverwrite** 속성에서 기존 데이터베이스를 덮어쓸지 여부를 결정 합니다. 경우는 **AllowOverwrite** 속성이 false로 설정 되어이 고 지정 된 데이터베이스가 이미 있으면 오류가 발생 합니다.  
  
 설정 해야 합니다 **파일** 의 속성을 **복원** 지정된 된 데이터베이스에 복원할 백업 파일에 대 한 UNC 경로 및 파일 이름으로 명령을. 설정할 수도 있습니다는 **암호** 지정된 된 백업 파일에 대 한 속성입니다. 경우는 **암호** 속성을 비어 있지 않은 값으로 설정 하면 지정된 된 암호를 사용 하 여 백업 파일이 해독 됩니다. 백업 파일이 암호화되지 않았거나 지정된 암호가 백업 파일을 암호화하는 데 사용된 암호와 일치하지 않으면 오류가 발생합니다.  
  
### <a name="restoring-security-settings"></a>보안 설정 복원  
 **보안** 속성에 따라 결정 하는지 여부를 합니다 **복원** 명령은 역할 및에 정의 된 권한과 같은 보안 정의 복원는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스. **보안** 속성 결정 하는지 여부를 합니다 **복원** Windows 사용자 계정 및 그룹 복원 프로세스의 일부로 보안 정의의 멤버로 정의 된 명령에 포함 되어 있습니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SkipMembership*|데이터베이스에 보안 정의는 포함되지만 멤버 정보는 제외됩니다.|  
|*CopyAll*|데이터베이스에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|데이터베이스에서 보안 정의가 제외됩니다.|  
  
### <a name="restoring-remote-partitions"></a>원격 파티션 복원  
 이전 하는 동안 만들어진 각 원격 백업 파일에 대 한 **백업** 명령을 포함 하 여 연결 된 해당 원격 파티션을 복원할 수 있습니다를 **위치** 요소에는 **위치**의 속성을 **복원** 명령입니다. 합니다 [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourcetype-element-xmla) 각각에 대 한 속성 **위치** 요소를 제외 되거나 명시적으로 설정 해야 *원격*합니다.  
  
 지정 된 각 **위치** 요소를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 연결에 지정 된 원격 데이터 원본의 합니다 **DataSourceID** 원격 백업 파일에 정의 된 파티션을 복원 하는 속성 에 지정 된 **파일** 속성입니다. 외에 합니다 **DataSourceID** 하 고 **파일** 속성을 다음 속성을 각각 사용할 수 있습니다 **위치** 원격 파티션을 복원 하는 데 사용 되는 요소:  
  
-   에 지정 된 원격 데이터 원본에 대 한 연결 문자열을 재정의 **DataSourceID**를 설정할 수 있습니다는 **ConnectionString** 속성을 **위치** 요소를를 다른 연결 문자열입니다. **복원** 명령을 사용 하 여에 포함 된 연결 문자열을 **ConnectionString** 속성입니다. 경우 **ConnectionString** 지정 하지 않으면 합니다 **복원** 명령은 지정 된 원격 데이터 원본에 대 한 백업 파일에 저장 된 연결 문자열을 사용 합니다. 사용할 수는 **ConnectionString** 설정을 원격 파티션을 다른 원격 인스턴스로 이동할 수 있습니다. 그러나 사용할 수 없습니다 합니다 **ConnectionString** 설정을 복원 된 데이터베이스가 있는 동일한 인스턴스에 원격 파티션을 복원할 수 있습니다. 즉, 사용할 수 없습니다는 **ConnectionString** 로컬 파티션에 원격 파티션을 만들 속성입니다.  
  
-   원격 데이터 원본의 원격 파티션을 저장 하는 데 각 원래 폴더를 지정할 수 있습니다는 [폴더](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla) 요소 원래 폴더에 저장 된 모든 원격 파티션을 복원할 새 폴더를 나타냅니다. 경우는 **폴더** 요소를 지정 하지 않으면 합니다 **복원** 명령에서는 원격 백업 파일에 포함 된 원격 파티션에 대해 지정 된 원래 폴더를 사용 합니다.  
  
### <a name="relocating-rolap-objects"></a>ROLAP 개체 재배치  
 합니다 **복원** 집계 또는 데이터 등의 정보는 기본 관계형 데이터 원본에서 테이블로 저장 되기 때문에 ROLAP 저장소를 사용 하는 개체에 대 한 명령으로 복원할 수 없습니다. 하지만 ROLAP 개체의 메타데이터는 복원할 수 있습니다. ROLAP 개체의 메타 데이터를 복원 하는 **복원** 명령에서는 관계형 데이터 원본에서 테이블 구조를 다시 만듭니다.  
  
 사용할 수는 **위치** 요소에는 **복원** ROLAP 개체 재배치 하는 명령입니다. 각 **위치** 데이터 원본을 재배치 하는 데 사용 되는 요소는 **DataSourceType** 속성 명시적으로 설정 해야 *로컬*합니다. 설정 해야 할 수도 있습니다는 **ConnectionString** 의 속성을 **위치** 새 위치의 연결 문자열로 요소. 복원 되는 동안는 **복원** 명령으로 식별 된 데이터 원본의 연결 문자열을 대체 합니다 **DataSourceID** 속성을 **위치** 요소 값을 사용 하 여는 **ConnectionString** 의 속성을 **위치** 요소입니다.  
  
##  <a name="synchronizing_databases"></a> 데이터베이스 동기화  
 **Synchronize** 명령은 데이터 및 지정 된 메타 데이터를 동기화 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다른 데이터베이스와 데이터베이스입니다. 합니다 **동기화** 명령에 다양 한 속성이 원본 데이터베이스를 지정할 수 있는 보안 정의 동기화 할 원격 파티션 및 ROLAP 개체의 동기화를 동기화 하는 방법.  
  
> [!NOTE]  
>  합니다 **동기화** 서버 관리자와 데이터베이스 관리자에 의해서만 명령을 실행할 수 있습니다. 원본 데이터베이스와 대상 데이터베이스의 데이터베이스 호환성 수준이 같아야 합니다.  
  
### <a name="specifying-the-source-database"></a>원본 데이터베이스 지정  
 [원본](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) 의 속성을 **동기화** 명령에는 두 개의 속성인 포함 됩니다. **ConnectionString** 및 **개체**합니다. 합니다 **ConnectionString** 원본 데이터베이스를 포함 하는 인스턴스의 연결 문자열을 포함 하는 속성 및 **개체** 속성 원본 데이터베이스에 대 한 개체 식별자를 포함 합니다.  
  
 대상 데이터베이스가 현재 데이터베이스는 세션에 대 한 합니다 **동기화** 명령을 실행 합니다.  
  
 경우는 **ApplyCompression** 의 속성을 **동기화** 명령 집합은 전송 되기 전에 대상 데이터베이스에는 데이터베이스의 압축 true 이면 원본에서 전송 되는 정보.  
  
### <a name="synchronizing-security-settings"></a>보안 설정 동기화  
 [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) 속성에 따라 결정 하는지 여부를 **동기화** 명령은 역할 및 원본 데이터베이스에 정의 된 권한과 같은 보안 정의 동기화 합니다. **SynchronizeSecurity** 속성 결정 하는지 여부를 합니다 **동기화 할** Windows 사용자 계정 및 그룹 보안 정의의 멤버로 정의 된 명령에 포함 되어 있습니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SkipMembership*|대상 데이터베이스에 보안 정의만 포함되고 멤버 정보는 제외됩니다.|  
|*CopyAll*|대상 데이터베이스에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|대상 데이터베이스에서 보안 정의가 제외됩니다.|  
  
### <a name="synchronizing-remote-partitions"></a>원격 파티션 동기화  
 원본 데이터베이스에 있는 각 원격 데이터 원본에 대해 연결 된 각 원격 파티션을 포함 하 여 동기화 수 있습니다는 **위치** 요소에는 **위치** 속성을  **동기화** 명령입니다. 각 **위치** 요소를 **DataSourceType** 속성을 제외 되거나 명시적으로 설정 해야 *원격*합니다.  
  
 정의 하 고 대상 데이터베이스에서 원격 데이터 원본에 연결 합니다 **동기화** 명령에 정의 된 연결 문자열을 사용 합니다 **ConnectionString** 속성은 **위치**  요소입니다. **동기화** 명령을 사용 하 여 다음는 **DataSourceID** 속성을 **위치** 동기화 할 원격 파티션을 식별 하는 요소입니다. 합니다 **동기화**명령에 지정 된 원격 데이터 원본의 원격 파티션을 동기화 합니다 **DataSourceID** 는에지정된원격데이터원본의원본데이터베이스의속성 **DataSourceID** 대상 데이터베이스의 속성입니다.  
  
 원본 데이터베이스에 있는 원격 데이터 원본의 원격 파티션을 저장 하는 데 각 원래 폴더를 지정할 수도 있습니다는 **폴더** 요소에는 **위치** 요소입니다. 합니다 **폴더** 요소는 원격 데이터 원본의 원래 폴더에 저장 된 모든 원격 파티션을 동기화 할 대상 데이터베이스에 대 한 새 폴더를 나타냅니다. 경우는 **폴더** 요소를 지정 하지 않으면 Synchronize 명령에서는 원본 데이터베이스에 포함 된 원격 파티션에 대해 지정 된 원래 폴더를 사용 합니다.  
  
### <a name="synchronizing-rolap-objects"></a>ROLAP 개체 동기화  
 합니다 **동기화** 명령 집계 또는 이러한 정보는 기본 관계형 데이터 원본에서 테이블로 저장 되기 때문에 ROLAP 저장소를 사용 하는 개체에 대 한 데이터를 동기화 할 수 없습니다. 하지만 ROLAP 개체의 메타데이터는 동기화할 수 있습니다. 메타 데이터를 동기화 하는 **동기화** 명령에서는 관계형 데이터 원본에서 테이블 구조를 다시 만듭니다.  
  
 사용할 수는 **위치** 명령의 ROLAP 개체를 동기화 하는 요소입니다. 각 **위치** 데이터 원본을 재배치 하는 데 사용 되는 요소는 **DataSourceType** 속성 명시적으로 설정 해야 *로컬*합니다. . 설정 해야 할 수도 있습니다는 **ConnectionString** 의 속성을 **위치** 새 위치의 연결 문자열로 요소. 동기화 하는 동안는 **동기화** 명령으로 식별 된 데이터 원본의 연결 문자열을 대체 합니다 **DataSourceID** 속성을 **위치** 값을 가진 요소를 **ConnectionString** 의 속성을 **위치** 요소.  
  
## <a name="see-also"></a>관련 항목  
 [Backup 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Restore 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Synchronize 요소&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Analysis Services 데이터베이스 백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  

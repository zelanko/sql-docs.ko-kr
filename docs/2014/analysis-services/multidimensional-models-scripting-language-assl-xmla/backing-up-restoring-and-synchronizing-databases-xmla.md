---
title: 데이터베이스 백업, 복원 및 동기화 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6163a538c4e8872016f7ec572e4c177cfe92de94
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702272"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>데이터베이스 백업, 복원 및 동기화(XMLA)
  XML for Analysis에는 데이터베이스를 백업, 복원 및 동기화하는 세 개의 명령이 있습니다.  
  
-   [Backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) 명령은 [데이터베이스 백업](#backing_up_databases) 섹션에 설명된 대로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]백업 파일 (. .abf)을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]데이터베이스를 백업합니다.  
  
-   [Restore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) 명령은 데이터베이스 [복원](#restoring_databases)섹션 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 설명 된 대로 .abf 파일에서 데이터베이스를 복원 합니다.  
  
-   [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) 명령은 데이터베이스 동기화 섹션 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 설명 된 대로 한 데이터베이스를 다른 데이터베이스의 데이터 및 메타 데이터와 동기화 [Synchronizing Databases](#synchronizing_databases)합니다.  
  
##  <a name="backing-up-databases"></a><a name="backing_up_databases"></a>데이터베이스 백업  
 앞에서 설명한 대로 `Backup` 명령에서는 지정된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 백업 파일에 백업합니다. `Backup` 명령에는 백업할 데이터베이스, 사용할 백업 파일, 보안 정의 백업 방법 및 백업할 원격 파티션을 지정할 수 있는 다양한 속성이 있습니다.  
  
> [!IMPORTANT]  
>  Analysis Services 서비스 계정에는 각 파일에 대해 지정한 백업 위치에 쓸 수 있는 권한이 있어야 합니다. 또한 사용자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 관리자 역할이나 백업할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버를 가지고 있어야 합니다.  
  
### <a name="specifying-the-database-and-backup-file"></a>데이터베이스 및 백업 파일 지정  
 백업할 데이터베이스를 지정 하려면 `Backup` 명령의 [개체](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 속성을 설정 합니다. `Object` 속성에는 데이터베이스에 대한 개체 식별자가 있어야 하며, 그렇지 않으면 오류가 발생합니다.  
  
 백업 프로세스에서 만들고 사용할 파일을 지정 하려면 `Backup` 명령의 [file](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla) 속성을 설정 합니다. `File` 속성은 만들 백업 파일에 대한 UNC 경로 및 파일 이름으로 설정되어야 합니다.  
  
 백업에 사용할 파일을 지정하는 것 외에도 지정된 백업 파일에 대해 다음과 같은 옵션을 설정할 수 있습니다.  
  
-   [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla) 속성을 true로 설정 하면 지정 된 파일이 `Backup` 이미 있는 경우 명령에서 백업 파일을 덮어씁니다. `AllowOverwrite` 속성을 false로 설정한 경우 지정된 백업 파일이 이미 있으면 오류가 발생합니다.  
  
-   [Applycompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla) 속성을 true로 설정 하면 파일을 만든 후 백업 파일이 압축 됩니다.  
  
-   [Password](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla) 속성을 비어 있지 않은 값으로 설정 하면 지정 된 암호를 사용 하 여 백업 파일이 암호화 됩니다.  
  
    > [!IMPORTANT]  
    >  `ApplyCompression` 및 `Password` 속성을 지정하지 않으면 연결 문자열에 포함된 사용자 이름 및 암호가 백업 파일에 일반 텍스트로 저장됩니다. 일반 텍스트로 저장된 데이터는 검색될 수 있으므로 보안을 강화하려면 `ApplyCompression` 및 `Password` 설정을 사용하여 백업 파일을 압축하고 암호화합니다.  
  
### <a name="backing-up-security-settings"></a>보안 설정 백업  
 [보안](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) 속성은 `Backup` 명령이 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 정의 된 역할 및 권한과 같은 보안 정의를 백업 하는지 여부를 결정 합니다. 또한 `Security` 속성에서는 보안 정의의 멤버로 정의된 Windows 사용자 계정 및 그룹을 백업 파일에 포함할지 여부도 결정합니다.  
  
 `Security` 속성의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|*SkipMembership*|백업 파일에 보안 정의는 포함되지만 멤버 정보는 제외됩니다.|  
|*CopyAll*|백업 파일에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|백업 파일에서 보안 정의가 제외됩니다.|  
  
### <a name="backing-up-remote-partitions"></a>원격 파티션 백업  
 데이터베이스의 원격 파티션을 백업 하려면 `Backup` 명령의 [backupremotepartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla) 속성을 true로 설정 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이렇게 설정하면 `Backup` 명령에서 데이터베이스의 원격 파티션을 저장하는 데 사용되는 각 원격 데이터 원본에 대해 원격 백업 파일을 만듭니다.  
  
 백업할 각 원격 데이터 원본에 대해 `Backup` 명령의 location 속성에 [Location](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla) 요소를 포함 하 여 해당 백업 파일을 지정할 수 있습니다 [Locations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla) . 요소의 속성은 원격 백업 파일의 UNC 경로 및 파일 이름으로 설정 되어야 하며, DataSourceID 속성은 데이터베이스에 정의 된 원격 데이터 원본의 식별자로 설정 되어야 합니다. [DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) `Location` `File`  
  
##  <a name="restoring-databases"></a><a name="restoring_databases"></a>데이터베이스 복원  
 `Restore` 명령은 백업 파일에서 지정된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원합니다. `Restore` 명령에는 복원할 데이터베이스, 사용할 백업 파일, 보안 정의 복원 방법, 저장할 원격 파티션 및 재배치 ROLAP(관계형 OLAP) 개체를 지정할 수 있는 다양한 속성이 있습니다.  
  
> [!IMPORTANT]  
>  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
### <a name="specifying-the-database-and-backup-file"></a>데이터베이스 및 백업 파일 지정  
 `DatabaseName` 명령의 `Restore` 속성에는 데이터베이스에 대한 개체 식별자가 있어야 하며, 그렇지 않으면 오류가 발생합니다. 지정된 데이터베이스가 이미 있으면 `AllowOverwrite` 속성에서 기존 데이터베이스를 덮어쓸지 여부를 결정합니다. `AllowOverwrite` 속성이 false이고 지정된 데이터베이스가 이미 있으면 오류가 발생합니다.  
  
 `File` 명령의 `Restore` 속성을 지정된 데이터베이스에 복원할 백업 파일의 UNC 경로 및 파일 이름으로 설정해야 합니다. 지정된 백업 파일에 대한 `Password` 속성을 설정할 수도 있습니다. `Password` 속성을 비어 있지 않은 값으로 설정하면 지정된 암호를 사용하여 백업 파일이 해독됩니다. 백업 파일이 암호화되지 않았거나 지정된 암호가 백업 파일을 암호화하는 데 사용된 암호와 일치하지 않으면 오류가 발생합니다.  
  
### <a name="restoring-security-settings"></a>보안 설정 복원  
 `Security` 속성에서는 `Restore` 명령을 실행할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 정의된 역할 및 권한과 같은 보안 정의를 복원할지 여부를 결정합니다. 또한 `Security` 속성에서는 복원 프로세스의 일부로 보안 정의의 멤버로 정의된 Windows 사용자 계정 및 그룹을 `Restore` 명령에 포함할지 여부를 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|*SkipMembership*|데이터베이스에 보안 정의는 포함되지만 멤버 정보는 제외됩니다.|  
|*CopyAll*|데이터베이스에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|데이터베이스에서 보안 정의가 제외됩니다.|  
  
### <a name="restoring-remote-partitions"></a>원격 파티션 복원  
 `Backup` 요소를 `Location` 명령의 `Locations` 속성에 포함하여 이전 `Restore` 명령 도중 만들어진 각 원격 백업 파일에 대해 연결된 해당 원격 파티션을 복원할 수 있습니다. 각 [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) `Location` 요소의 DataSourceType 속성은 제외 되거나 명시적으로 *Remote*로 설정 되어야 합니다.  
  
 지정된 각 `Location` 요소에 대해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 `DataSourceID` 속성에 지정된 원격 데이터 원본을 연결하여 `File` 속성에 지정된 원격 백업 파일에 정의된 파티션을 복원합니다. 각 `DataSourceID` 요소에서는 `File` 및 `Location` 속성 외에도 다음과 같은 속성을 사용하여 원격 파티션을 복원할 수 있습니다.  
  
-   `DataSourceID`에 지정된 원격 데이터 원본에 대한 연결 문자열을 재정의하기 위해 `ConnectionString` 요소의 `Location` 속성을 다른 연결 문자열로 설정할 수 있습니다. 그런 다음 `Restore` 명령에서는 `ConnectionString` 속성에 포함된 연결 문자열을 사용합니다. `ConnectionString`이 지정되지 않은 경우 `Restore` 명령에서는 지정된 원격 데이터 원본에 대한 백업 파일에 저장된 연결 문자열을 사용합니다. `ConnectionString` 설정을 사용하여 원격 파티션을 다른 원격 인스턴스로 이동할 수 있습니다. 하지만 `ConnectionString` 설정을 사용하여 복원된 데이터베이스가 들어 있는 동일한 인스턴스에 원격 파티션을 복원할 수는 없습니다. 다시 말해서 `ConnectionString` 속성을 사용하여 로컬 파티션에 원격 파티션을 만들 수 없습니다.  
  
-   원격 데이터 원본에 원격 파티션을 저장 하는 데 사용 되는 각 원래 폴더에 대해 [폴더](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla) 요소를 지정 하 여 원래 폴더에 저장 된 모든 원격 파티션을 복원할 새 폴더를 나타낼 수 있습니다. `Folder` 요소를 지정하지 않은 경우 `Restore` 명령에서는 원격 백업 파일에 포함된 원격 파티션에 대해 지정된 원래 폴더를 사용합니다.  
  
### <a name="relocating-rolap-objects"></a>ROLAP 개체 재배치  
 ROLAP 스토리지를 사용하는 개체에 대한 집계 또는 데이터는 내부 관계형 데이터 원본에서 테이블로 저장되므로 이러한 정보는 `Restore` 명령으로 복원할 수 없습니다. 하지만 ROLAP 개체의 메타데이터는 복원할 수 있습니다. ROLAP 개체의 메타데이터를 복원하기 위해 `Restore` 명령에서는 관계형 데이터 원본의 테이블 구조를 다시 만듭니다.  
  
 `Location` 명령의 `Restore` 요소를 사용하여 ROLAP 개체를 재배치할 수 있습니다. 데이터 원본을 `Location` 재배치 하는 데 사용 되는 각 요소 `DataSourceType` 에 대해 속성을 명시적으로 *Local*로 설정 해야 합니다. 또한 `ConnectionString` 요소의 `Location` 속성을 새 위치의 연결 문자열로 설정해야 합니다. 복원되는 동안 `Restore` 명령에서는 `DataSourceID` 요소의 `Location` 속성으로 식별된 데이터 원본의 연결 문자열을 `ConnectionString` 요소의 `Location` 속성 값으로 바꿉니다.  
  
##  <a name="synchronizing-databases"></a><a name="synchronizing_databases"></a>데이터베이스 동기화  
 `Synchronize` 명령에서는 지정된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 데이터 및 메타데이터를 다른 데이터베이스와 동기화합니다. `Synchronize` 명령에는 원본 데이터베이스, 보안 정의 동기화 방법, 동기화할 원격 파티션 및 ROLAP 개체의 동기화를 지정할 수 있는 다양한 속성이 있습니다.  
  
> [!NOTE]  
>  `Synchronize` 명령은 서버 관리자와 데이터베이스 관리자만 실행할 수 있습니다. 원본 데이터베이스와 대상 데이터베이스의 데이터베이스 호환성 수준이 같아야 합니다.  
  
### <a name="specifying-the-source-database"></a>원본 데이터베이스 지정  
 `Synchronize` 명령의 [Source](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) 속성에는 `ConnectionString` 및 `Object`라는 두 개의 속성이 있습니다. `ConnectionString` 속성에는 원본 데이터베이스가 포함된 인스턴스의 연결 문자열이 들어 있고, `Object` 속성에는 원본 데이터베이스의 개체 식별자가 들어 있습니다.  
  
 대상 데이터베이스는 세션에서 `Synchronize` 명령이 실행되는 현재 데이터베이스입니다.  
  
 `ApplyCompression` 명령의 `Synchronize` 속성이 true이면 원본 데이터베이스에서 대상 데이터베이스로 전송되는 정보는 압축된 후 전송됩니다.  
  
### <a name="synchronizing-security-settings"></a>보안 설정 동기화  
 [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) 속성은 명령에서 `Synchronize` 원본 데이터베이스에 정의 된 역할 및 권한과 같은 보안 정의를 동기화할지 여부를 결정 합니다. 또한 `SynchronizeSecurity` 속성에서는 보안 정의의 멤버로 정의된 Windows 사용자 계정 및 그룹을 `Sychronize` 명령에 포함할지 여부도 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|*SkipMembership*|대상 데이터베이스에 보안 정의만 포함되고 멤버 정보는 제외됩니다.|  
|*CopyAll*|대상 데이터베이스에 보안 정의와 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|대상 데이터베이스에서 보안 정의가 제외됩니다.|  
  
### <a name="synchronizing-remote-partitions"></a>원격 파티션 동기화  
 `Location` 요소를 `Locations` 명령의 `Synchronize` 속성에 포함하여 원본 데이터베이스에 있는 각 원격 데이터 원본에 대해 연결된 각 원격 파티션을 동기화할 수 있습니다. 각 `Location` 요소에 대해 `DataSourceType` 속성을 제외 하거나 명시적으로 *Remote*로 설정 해야 합니다.  
  
 대상 데이터베이스의 원격 데이터 원본을 정의하고 연결하기 위해 `Synchronize` 명령에서는 `ConnectionString` 요소의 `Location` 속성에 정의된 연결 문자열을 사용합니다. 그런 다음 `Synchronize` 명령에서는 `DataSourceID` 요소의 `Location` 속성을 사용하여 동기화할 원격 파티션을 식별합니다. 이 `Synchronize`명령은 원본 데이터베이스의 `DataSourceID` 속성에 지정 된 원격 데이터 원본의 원격 파티션을 대상 데이터베이스의 `DataSourceID` 속성에 지정 된 원격 데이터 원본과 동기화 합니다.  
  
 원본 데이터베이스에 있는 원격 데이터 원본의 원격 파티션을 저장하는 데 사용된 원래 폴더에 대해 각각 `Folder` 요소의 `Location` 요소를 지정할 수도 있습니다. `Folder` 요소는 원격 데이터 원본의 원래 폴더에 저장된 모든 원격 파티션을 동기화할 대상 데이터베이스의 새 폴더를 나타냅니다. `Folder` 요소가 지정되지 않은 경우 Synchronize 명령에서는 원격 데이터베이스에 포함된 원격 파티션에 대해 지정된 원래 폴더를 사용합니다.  
  
### <a name="synchronizing-rolap-objects"></a>ROLAP 개체 동기화  
 ROLAP 스토리지를 사용하는 개체에 대한 집계 또는 데이터는 내부 관계형 데이터 원본에서 테이블로 저장되므로 이러한 정보는 `Synchronize` 명령으로 동기화할 수 없습니다. 하지만 ROLAP 개체의 메타데이터는 동기화할 수 있습니다. 메타데이터를 동기화하기 위해 `Synchronize` 명령에서는 관계형 데이터 원본의 테이블 구조를 다시 만듭니다.  
  
 Synchronize 명령의 `Location` 요소를 사용하여 ROLAP 개체를 동기화할 수 있습니다. 데이터 원본을 `Location` 재배치 하는 데 사용 되는 각 요소 `DataSourceType` 에 대해 속성을 명시적으로 *Local*로 설정 해야 합니다. . 또한 `ConnectionString` 요소의 `Location` 속성을 새 위치의 연결 문자열로 설정해야 합니다. 동기화하는 동안 `Synchronize` 명령에서는 `DataSourceID` 요소의 `Location` 속성으로 식별된 데이터 원본의 연결 문자열을 `ConnectionString` 요소의 `Location` 속성 값으로 바꿉니다.  
  
## <a name="see-also"></a>참고 항목  
 [Backup 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Restore 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [XMLA &#40;요소 동기화&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Analysis Services 데이터베이스 백업 및 복원](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
